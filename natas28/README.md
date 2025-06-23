# Natas28 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas28
Password: 1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
URL:      http://natas28.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Whack Computer Joke Database.

  ```
  <body>
  <!--
      morla/10111
      y0 n0th!
  -->
  <h1>natas28</h1>
  <div id="content">
  
  <form action="index.php" method="POST">
      <h2> Whack Computer Joke Database</h2>
      Search: <input name="query"><br>
      <input type="submit" value="search" />
  </form>
  
  
  <div id="viewsource">sorry, we are currently out of sauce</div>
  </div>
  </body>
  ```

- Script will do the job, you can find exploitation details in script comments.

  ```
  $ python3 natas28-sql.py  
  <h2> Whack Computer Joke Database</h2><ul><li>natas29:31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns</li></ul>
  ```

---

## 🏁 Password for the next level

`Password for natas29 is: 31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
