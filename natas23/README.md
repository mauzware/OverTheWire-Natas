# Natas23 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas23
Password: dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
URL:      http://natas23.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- You will be prompted to input a password.

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
  <script>var wechallinfo = { "level": "natas23", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas23</h1>
  <div id="content">
  
  Password:
  <form name="input" method="get">
      <input type="text" name="passwd" size=20>
      <input type="submit" value="Login">
  </form>
  
  <?php
      if(array_key_exists("passwd",$_REQUEST)){
          if(strstr($_REQUEST["passwd"],"iloveyou") && ($_REQUEST["passwd"] > 10 )){
              echo "<br>The credentials for the next level are:<br>";
              echo "<pre>Username: natas24 Password: <censored></pre>";
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

- What’s happening here?

PHP condition:

```
if (strstr($_REQUEST["passwd"], "iloveyou") && ($_REQUEST["passwd"] > 10))
```

Key points:

- `strstr(...)` checks if `"iloveyou"` is *anywhere* in the input.
- Then it checks if `$_REQUEST["passwd"] > 10`. **BUT** PHP is loose with types:
    - If you pass something like `"iloveyou"` — it becomes `0` when compared numerically.
    - If you pass something like `"11iloveyou"` — it gets converted to `11`, because PHP reads the start of the string numerically.
    - `"iloveyou"` alone becomes `0` → `0 > 10` → false.

---

- Goal:

Send a value that:

1. **Contains** `"iloveyou"` → satisfies `strstr(...)`
2. **Evaluates as greater than 10** numerically → PHP type juggling

- Payload: `http://natas23.natas.labs.overthewire.org/?passwd=11iloveyou`

  <img src=""/>

---

## 🏁 Password for the next level

`Username: natas24 Password: MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
