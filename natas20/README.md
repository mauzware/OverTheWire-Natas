# Natas20 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas20
Password: p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
URL:      http://natas20.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Here, we have to login as admin again.

  ```
  <?php

  function debug($msg) { /* {{{ */
      if(array_key_exists("debug", $_GET)) {
          print "DEBUG: $msg<br>";
      }
  }
  /* }}} */
  function print_credentials() { /* {{{ */
      if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
      print "You are an admin. The credentials for the next level are:<br>";
      print "<pre>Username: natas21\n";
      print "Password: <censored></pre>";
      } else {
      print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas21.";
      }
  }
  /* }}} */
  
  /* we don't need this */
  function myopen($path, $name) {
      //debug("MYOPEN $path $name");
      return true;
  }
  
  /* we don't need this */
  function myclose() {
      //debug("MYCLOSE");
      return true;
  }
  
  function myread($sid) {
      debug("MYREAD $sid");
      if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
      debug("Invalid SID");
          return "";
      }
      $filename = session_save_path() . "/" . "mysess_" . $sid;
      if(!file_exists($filename)) {
          debug("Session file doesn't exist");
          return "";
      }
      debug("Reading from ". $filename);
      $data = file_get_contents($filename);
      $_SESSION = array();
      foreach(explode("\n", $data) as $line) {
          debug("Read [$line]");
      $parts = explode(" ", $line, 2);
      if($parts[0] != "") $_SESSION[$parts[0]] = $parts[1];
      }
      return session_encode() ?: "";
  }
  
  function mywrite($sid, $data) {
      // $data contains the serialized version of $_SESSION
      // but our encoding is better
      debug("MYWRITE $sid $data");
      // make sure the sid is alnum only!!
      if(strspn($sid, "1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM-") != strlen($sid)) {
      debug("Invalid SID");
          return;
      }
      $filename = session_save_path() . "/" . "mysess_" . $sid;
      $data = "";
      debug("Saving in ". $filename);
      ksort($_SESSION);
      foreach($_SESSION as $key => $value) {
          debug("$key => $value");
          $data .= "$key $value\n";
      }
      file_put_contents($filename, $data);
      chmod($filename, 0600);
      return true;
  }
  
  /* we don't need this */
  function mydestroy($sid) {
      //debug("MYDESTROY $sid");
      return true;
  }
  /* we don't need this */
  function mygarbage($t) {
      //debug("MYGARBAGE $t");
      return true;
  }
  
  session_set_save_handler(
      "myopen",
      "myclose",
      "myread",
      "mywrite",
      "mydestroy",
      "mygarbage");
  session_start();
  
  if(array_key_exists("name", $_REQUEST)) {
      $_SESSION["name"] = $_REQUEST["name"];
      debug("Name set to " . $_REQUEST["name"]);
  }
  
  print_credentials();
  
  $name = "";
  if(array_key_exists("name", $_SESSION)) {
      $name = $_SESSION["name"];
  }
  
  ?>
  ```

- They mentioned `debug` in the source code so I checked it out. Debug message indicates session file doesn’t exist. However, reloading the page reads from the session file.

- I intercepted the request and changed the `name` parameter to `%0Aadmin 1` instead of `admin`. Send the request two times in order to get a password for the next level.

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas20/burp.png"/>

---

## 🏁 Password for the next level

`Password for natas21 is: BPhv63cKE1lkQl04cE5CuFTzXe15NfiH`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
