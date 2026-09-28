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
🔎 Solution
1️⃣ Reverse Base64 Encoding

The first hint tells us:

Hint: Try reversing: base64

The input is Base64 encoded, so we need to decode it.

Command
base64 -d

Or:

echo "KXBwMDhxNzdwLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShsenJxbnBu" | base64 -d
Output
)pp08q77p-fa01g@ze0sfa4eG-gk3g-ta1ferirE(lzrqnpn
2️⃣ Reverse the Text

The next transformation was reversing the text.

The Linux command rev reverses the characters of a string.

Command
echo ")pp08q77p-fa01g@ze0sfa4eG-gk3g-ta1ferirE(lzrqnpn" | rev
Output
npnqrzl(Eriref1at-g3kg-Ge4afs0ez@g10af-p77q80pp)
3️⃣ Replace - with _

The challenge tells us that underscores were previously replaced with dashes.

Therefore, we reverse:

-  →  _

The Linux tr command is useful for character substitution.

Command
echo "npnqrzl(Eriref1at-g3kg-Ge4afs0ez@g10af-p77q80pp)" | tr '-' '_'
Output
npnqrzl(Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp)
4️⃣ Replace Parentheses with Curly Braces

The original curly braces were transformed into parentheses.

Therefore:

(  →  {
)  →  }
Command
echo "npnqrzl(Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp)" | tr '()' '{}'
Output
npnqrzl{Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp}
5️⃣ Reverse ROT13

The final transformation was ROT13.

ROT13 is special because applying it twice returns the original text.

So we can use ROT13 again to reverse it.

Command
echo "npnqrzl{Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
Output
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
🚩 Flag
<div align="center">
🎉 Challenge Solved!
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
</div>
🔄 Transformation Chain

The complete reverse process was:

┌─────────────────────────────────────────────────────┐
│                  Encoded String                     │
└──────────────────────┬──────────────────────────────┘
                       ↓
                 Base64 Decode
                       ↓
                     rev
                       ↓
                    - → _
                       ↓
                   () → {}
                       ↓
                    ROT13
                       ↓
┌──────────────────────┴──────────────────────────────┐
│                 Original Flag                       │
└─────────────────────────────────────────────────────┘
In Short
Base64
   ↓
base64 -d
   ↓
rev
   ↓
tr '-' '_'
   ↓
tr '()' '{}'
   ↓
ROT13
   ↓
🚩 FLAG
🛠️ Commands Used
Command	Purpose
base64 -d	Decode Base64
rev	Reverse characters
tr '-' '_'	Replace dashes with underscores
tr '()' '{}'	Replace parentheses with curly braces
tr 'A-Za-z' 'N-ZA-Mn-za-m'	Apply ROT13
🧠 What I Learned
🔹 base64

Base64 is commonly used to represent binary/text data using printable characters.

base64 -d

is used to decode Base64 data.

🔹 rev

The rev command reverses the characters of each line.

Example:

echo "hello" | rev

Output:

olleh
🔹 tr

tr is a Linux command used for translating or replacing characters.

Example:

echo "hello-world" | tr '-' '_'

Output:

hello_world
🔹 ROT13

ROT13 shifts each alphabetic character by 13 positions.

Example:

hello → uryyb

Because ROT13 is reversible:

hello → ROT13 → uryyb → ROT13 → hello
💡 Key Takeaway

The main lesson from this challenge is:

When reversing multiple transformations, always undo them in the opposite order in which they were applied.

This challenge provided a simple but useful introduction to Linux text-processing commands and basic encoding/obfuscation techniques.

📚 Skills Practiced
🐧 Linux Command Line
🔐 Base64 Encoding / Decoding
🔄 Text Reversal
🔤 Character Translation
🔑 ROT13
🧩 CTF Problem Solving
🏁 Conclusion

The Undo challenge demonstrates how several simple transformations can make
a string appear complicated.

By identifying each transformation and reversing them systematically, the
original flag can be recovered.

Final Flag
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
<p align="center">

⭐ <b>picoCTF 2026 — Undo</b> ⭐

<br>

<i>Learn • Practice • Break • Understand • Repeat</i>

</p> ```
✨ For your GitHub

I recommend keeping your repository structure like this:

picoCTF-2026/
│
├── General-Skills/
│   │
│   └── Undo/
│       ├── README.md
│       └── screenshot.png
│
└── README.md

And your GitHub page will then have a much cleaner CTF write-up appearance, with the challenge information at the top, commands in terminal blocks, a transformation diagram, and the flag clearly separated at the end.
