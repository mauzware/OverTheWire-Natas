# Natas15 — OverTheWire

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

## 📸 Credentials

```
Username: natas15
Password: SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
URL:      http://natas15.natas.labs.overthewire.org
```

---

## 🧠 Walkthrough

- Access the site using credentials.

- We are still on SQLI section. Here, it's exactly the same as in the last level, just with more sanitization.

- You can try to find a right payload manually, but here I wrote a script for getting the password.

  ```
  $ python3 sqli-session.py                                                                                  
  Trying: a
  Trying: b
  Trying: c
  Trying: d
  Trying: e
  Trying: f
  Trying: g
  Trying: h
  [SNIP!]
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGi
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGj
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGk
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGl
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGm
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGn
  Trying with: hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
  ```
  
- Last string is the actual password for natas16.

---

## 🏁 Password for the next level

`Password for natas16 is hPkjKYviLQctEW33QmuXL6eDVfMW4sGo`

---

Back to [Main Repo](https://github.com/mauzware/OverTheWire-Natas)
