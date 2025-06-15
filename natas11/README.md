# Natas11 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas11
Password: UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
URL: http://natas11.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.
- When you open developer tools, you will see an encoded XOR cookie.

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas11/cookie.png"/>
  
- It is also reflected in the source code.

  ```
  <?

  $defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");
  
  function xor_encrypt($in) {
      $key = '<censored>';
      $text = $in;
      $outText = '';
  
      // Iterate through each character
      for($i=0;$i<strlen($text);$i++) {
      $outText .= $text[$i] ^ $key[$i % strlen($key)];
      }
  
      return $outText;
  }
  
  function loadData($def) {
      global $_COOKIE;
      $mydata = $def;
      if(array_key_exists("data", $_COOKIE)) {
      $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
      if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {
          if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) {
          $mydata['showpassword'] = $tempdata['showpassword'];
          $mydata['bgcolor'] = $tempdata['bgcolor'];
          }
      }
      }
      return $mydata;
  }
  
  function saveData($d) {
      setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
  }
  
  $data = loadData($defaultdata);
  
  if(array_key_exists("bgcolor",$_REQUEST)) {
      if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor'])) {
          $data['bgcolor'] = $_REQUEST['bgcolor'];
      }
  }
  
  saveData($data);
  
  
  
  ?>
  
  <h1>natas11</h1>
  <div id="content">
  <body style="background: <?=$data['bgcolor']?>;">
  Cookies are protected with XOR encryption<br/><br/>
  
  <?
  if($data["showpassword"] == "yes") {
      print "The password for natas12 is <censored><br>";
  }
  
  ?>
  ```

- You have to get a Key for XOR then use that key on `showpassword` and encrypt it with XOR then Base64 and paste that value into cookie value. So, I wrote PHP script in order to get XOR Key.

  ```
  php XORcookie.php      
  eDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoe
  ```

- Key is `eDWo`. Now, I wrote another PHP script in order to get the cookie value.

  ```
  php gettingCookie.php     
  HmYkBwozJw4WNyAAFyB1VUc9MhxHaHUNAic4Awo2dVVHZzEJAyIxCUc5
  ```

- Replace the original cookie value with the new one and BOOM! You got a password.

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas11/pw.png"/>

---

## 🏁 Password for the next level

`The password for natas12 is yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
