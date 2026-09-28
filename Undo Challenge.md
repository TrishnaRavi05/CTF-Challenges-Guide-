# 🧩 picoCTF 2026 — Undo

> **Can you reverse a series of Linux text transformations to recover the original flag?**

<p align="center">

![picoCTF](https://img.shields.io/badge/picoCTF-2026-orange?style=for-the-badge)
![Category](https://img.shields.io/badge/Category-General%20Skills-blue?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-Commands-black?style=for-the-badge)

</p>

---

## 📌 Challenge Information

| Information | Details |
|---|---|
| 🏆 Platform | picoCTF 2026 |
| 🧩 Challenge | Undo |
| 📂 Category | General Skills |
| 🟢 Difficulty | Easy |
| 🛠️ Skills | Linux, Base64, `rev`, `tr`, ROT13 |

---

## 🎯 Objective

The challenge gives us a string that has been transformed multiple times using
different Linux text-processing techniques.

Our goal is to **reverse every transformation in the correct order** and recover
the original flag.

### Initial Encoded String

```text
KXBwMDhxNzdwLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShsenJxbnBu
