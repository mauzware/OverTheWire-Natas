# Natas6 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas6
Password: 0RoJwHdSKWFTYR5WuiAewauSuNaBXned
URL: http://natas6.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

1. Access the site using credentials.
2. You will be asked to input a secret
3. Here's the source code.

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
  <script>var wechallinfo = { "level": "natas6", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas6</h1>
  <div id="content">
  
  <?
  
  include "includes/secret.inc";
  
      if(array_key_exists("submit", $_POST)) {
          if($secret == $_POST['secret']) {
          print "Access granted. The password for natas7 is <censored>";
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
   
4. After visiting `/secret`, you will get a blank page which you can confirm in Burp as well. `304 NOT MODIFIED` tell's us to edit the request.

<img src=""/>

5. Now, remove `If-Modified-Since` and `If-None-Match` from the request and send it back to get a secret that you need to input in order to get a pssword.

<img src=""/>

---

## 🏁 Password for the next level

`Access granted. The password for natas7 is bmg8SvU1LizuWjx3y7xkNERkHxGre0GS`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
