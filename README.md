# OverTheWire — Natas Walkthroughs 

[<img align='center' src="https://github.com/mauzware/mauzware/blob/main/BANNER.png" width="100%"/>](https://github.com/mauzware)

Welcome to my [OverTheWire: Natas](https://overthewire.org/wargames/natas/) writeup archive. This series of challenges focuses on web security and HTTP, and offers a great step-by-step approach to learning web exploitation techniques.

All challenges were solved in a safe, legal, and educational environment. These write-ups are intended to help others learn, not to encourage misuse.

---

## 🔧 Tools & Setup
- Burp Suite
- [Python & PHP scripts](https://github.com/mauzware/Random-Scripts/tree/main/Natas)
- curl & wget
- Web proxies & debugging
- Your brain 🧠

---

## Official Description

Natas teaches the basics of serverside web-security.

Each level of natas consists of its own website located at http://natasX.natas.labs.overthewire.org, where X is the level number. There is no SSH login. To access a level, enter the username for that level (e.g. natas0 for level 0) and its password.

Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. All passwords are also stored in /etc/natas_webpass/. 
E.g. the password for natas5 is stored in the file /etc/natas_webpass/natas5 and only readable by natas4 and natas5.

---

## 📜 Walkthroughs

| Level | Link |
|-------|------|
| Natas0 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas0) |
| Natas1 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas1) |
| Natas2 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas2) |
| Natas3 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas3) |
| Natas4 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas4) |
| Natas5 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas5) |
| Natas6 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas6) |
| Natas7 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas7) |
| Natas8 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas8) |
| Natas9 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas9) |
| Natas10 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas10) |
| Natas11 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas11) |
| Natas12 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas12) |
| Natas13 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas13) |
| Natas14 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas14) |
| Natas15 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas15) |
| Natas16 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas16) |
| Natas17 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas17) |
| Natas18 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas18) |
| Natas19 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas19) |
| Natas20 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas20) |
| Natas21 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas21) |
| Natas22 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas22) |
| Natas23 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas23) |
| Natas24 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas24) |
| Natas25 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas25) |
| Natas26 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas26) |
| Natas27 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas27) |
| Natas28 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas28) |
| Natas29 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas29) |
| Natas30 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas30) |
| Natas31 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas31) |
| Natas32 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas32) |
| Natas33 | [View Walkthrough](https://github.com/mauzware/OverTheWire-Natas/tree/main/natas33) |

<img src="https://github.com/mauzware/OverTheWire-Natas/blob/main/natas33/congrats.png"/>

If you're doing Natas too — good luck!

---

## ⛔️ License

This repository is licensed under the [CC BY-NC-ND 4.0 License](https://creativecommons.org/licenses/by-nc-nd/4.0/).  
You are free to read and share the content with attribution, but reuse, modification, or redistribution is not allowed.

These are personal notes and CTF writeups meant for educational purposes only.<br>
Please do not copy, republish, or claim this work as your own.

More info: [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)

---

## 👋 Follow my journey

If you liked this walkthroughs, feel free to follow me on:

<a href="https://medium.com/@mauzware"><img src="https://img.shields.io/badge/Medium-style?style=for-the-badge&logo=medium&color=black" alt="Medium"/></a>
<a href="https://www.linkedin.com/in/filip-milenkovic-576a73228/"><img src="https://img.shields.io/badge/LinkedIn-style?style=for-the-badge&color=blue" alt="LinkedIn"/></a>
<a href="https://github.com/mauzware"><img src="https://img.shields.io/badge/GitHub-style?style=for-the-badge&logo=github&color=black" alt="GitHub"/></a>

---

⚠️ **Disclaimer: The content in this repository is for educational and informational purposes only; the author holds no responsibility for misuse. 
Ensure proper authorization before use, act responsibly at your own risk, and comply with all legal and ethical guidelines.** ⚠️

