# Natas8 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas8
Password: xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
URL: http://natas8.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- Again, you have to input a secret. It's revealed in the source code

  ```
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas8", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas8</h1>
  <div id="content">
  
  <?
  
  $encodedSecret = "3d3d516343746d4d6d6c315669563362";
  
  function encodeSecret($secret) {
      return bin2hex(strrev(base64_encode($secret)));
  }
  
  if(array_key_exists("submit", $_POST)) {
      if(encodeSecret($_POST['secret']) == $encodedSecret) {
      print "Access granted. The password for natas9 is <censored>";
      } else {
      print "Wrong secret";
      }
  }
  ?>
  
  <form method=post>
  Input secret: <input name=secret><br>
  <input type=submit name=submit>
  </form>
  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- This is the encoded secret: `3d3d516343746d4d6d6c315669563362`. Its hex, then reverse, then base64 and you get this `oubWYf2kBq`.

- Input the decoded string and you will get a password.

---

## 🏁 Password for the next level

`Access granted. The password for natas9 is ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t `

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
