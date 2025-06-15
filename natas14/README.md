# Natas14 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas14
Password: z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
URL:      http://natas14.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- SQL INJECTION TIME LEGOOOOOOO.

  ```
  <body>
  <h1>natas14</h1>
  <div id="content">
  <?php
  if(array_key_exists("username", $_REQUEST)) {
      $link = mysqli_connect('localhost', 'natas14', '<censored>');
      mysqli_select_db($link, 'natas14');
  
      $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";
      if(array_key_exists("debug", $_GET)) {
          echo "Executing query: $query<br>";
      }
  
      if(mysqli_num_rows(mysqli_query($link, $query)) > 0) {
              echo "Successful login! The password for natas15 is <censored><br>";
      } else {
              echo "Access denied!<br>";
      }
      mysqli_close($link);
  } else {
  ?>
  
  <form action="index.php" method="POST">
  Username: <input name="username"><br>
  Password: <input name="password"><br>
  <input type="submit" value="Login" />
  </form>
  <?php } ?>
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```
  
- This payload worked for me `" or ""="`. Put it in both username and password and you'll get a password for the next level.

---

## 🏁 Password for the next level

`natas15 password is SdqIqBsFcz3yotlNYErZSZwblkm0lrvx`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
