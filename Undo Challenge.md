# 🧩 picoCTF 2026 — Undo

> 🔐 Can you reverse a series of Linux text transformations to recover the original flag?

<p align="center">

![picoCTF](https://img.shields.io/badge/picoCTF-2026-orange?style=for-the-badge)
![Category](https://img.shields.io/badge/Category-General%20Skills-blue?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-Commands-black?style=for-the-badge)

</p>

---

## 📌 Challenge Information

| 🏷️ Property | 📋 Details |
|---|---|
| 🏆 Platform | picoCTF 2026 |
| 🧩 Challenge | Undo |
| 📂 Category | General Skills |
| 🟢 Difficulty | Easy |
| 🐧 Environment | Linux |
| 🛠️ Tools | `base64`, `rev`, `tr` |

---

## 🎯 Objective

The challenge provides a string that has been transformed using multiple
Linux text-processing operations.

The goal is to **reverse each transformation in the correct order** and
recover the original flag.

### 🔑 Initial Encoded String

```text
KXBwMDhxNzdwLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShsenJxbnBu
```

### 💡 Important Concept

> 🔄 When reversing multiple transformations, undo them in the **opposite order** in which they were originally applied.

---

# 🔎 Solution

## 1️⃣ Reverse Base64 Encoding

The first hint provided by the challenge was:

```text
Hint: Try reversing: base64
```

The input is Base64 encoded, so we need to decode it.

### 💻 Command

```bash
base64 -d
```

Or directly:

```bash
echo "KXBwMDhxNzdwLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShsenJxbnBu" | base64 -d
```

### 📤 Output

```text
)pp08q77p-fa01g@ze0sfa4eG-gk3g-ta1ferirE(lzrqnpn
```

---

## 2️⃣ Reverse the Text

The next transformation was reversing the text.

Linux provides the `rev` command to reverse the characters of a string.

### 💻 Command

```bash
echo ")pp08q77p-fa01g@ze0sfa4eG-gk3g-ta1ferirE(lzrqnpn" | rev
```

### 📤 Output

```text
npnqrzl(Eriref1at-g3kg-Ge4afs0ez@g10af-p77q80pp)
```

---

## 3️⃣ Replace `-` with `_`

The challenge states that underscores were replaced with dashes.

Therefore, we need to reverse:

```text
-  →  _
```

The `tr` command can be used for character substitution.

### 💻 Command

```bash
echo "npnqrzl(Eriref1at-g3kg-Ge4afs0ez@g10af-p77q80pp)" | tr '-' '_'
```

### 📤 Output

```text
npnqrzl(Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp)
```

---

## 4️⃣ Replace Parentheses with Curly Braces

The challenge states that curly braces were replaced with parentheses.

Therefore:

```text
(  →  {
)  →  }
```

### 💻 Command

```bash
echo "npnqrzl(Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp)" | tr '()' '{}'
```

### 📤 Output

```text
npnqrzl{Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp}
```

---

## 5️⃣ Reverse ROT13

The final transformation was ROT13.

The challenge tells us:

```text
Hint: Applied ROT13 to letters.
```

ROT13 shifts each alphabetic character by 13 positions.

An important property of ROT13 is that it is **self-reversing**:

```text
ROT13(ROT13(text)) = text
```

Therefore, applying ROT13 again will recover the original text.

### 💻 Command

```bash
echo "npnqrzl{Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### 📤 Output

```text
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
```

---

# 🚩 Flag

<div align="center">

### 🎉 Challenge Solved!

```text
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
```

</div>

---

# 🔄 Transformation Chain

The complete reverse process can be summarized as:

```text
Encoded String
      │
      ▼
Base64 Decode
      │
      ▼
     rev
      │
      ▼
   - → _
      │
      ▼
   () → {}
      │
      ▼
    ROT13
      │
      ▼
Original Flag
```

### ⚡ Quick Summary

```text
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
```

---

# 🛠️ Commands Used

| Command | Purpose |
|---|---|
| `base64 -d` | Decode Base64 data |
| `rev` | Reverse characters |
| `tr '-' '_'` | Convert dashes to underscores |
| `tr '()' '{}'` | Convert parentheses to curly braces |
| `tr 'A-Za-z' 'N-ZA-Mn-za-m'` | Apply ROT13 |

---

# 🧠 What I Learned

### 🐧 1. Base64

Base64 is a common encoding technique used to represent data using printable characters.

The following command decodes Base64:

```bash
base64 -d
```

---

### 🔄 2. `rev`

The `rev` command reverses the characters in each line.

Example:

```bash
echo "hello" | rev
```

Output:

```text
olleh
```

---

### 🔤 3. `tr`

The `tr` command is useful for translating or replacing characters.

Example:

```bash
echo "hello-world" | tr '-' '_'
```

Output:

```text
hello_world
```

---

### 🔐 4. ROT13

ROT13 shifts every alphabetic character by 13 positions.

For example:

```text
hello → uryyb
```

Applying ROT13 again gives:

```text
uryyb → hello
```

---

# 💡 Key Takeaway

The most important concept from this challenge is:

> **When reversing a sequence of transformations, always work backwards from the final transformation to the first.**

This challenge provided practical experience with:

- 🐧 Linux command-line utilities
- 🔐 Base64 encoding/decoding
- 🔄 String reversal
- 🔤 Character substitution
- 🔑 ROT13
- 🧩 CTF problem solving

---

# 🏁 Conclusion

The **Undo** challenge demonstrates how multiple simple text transformations can make a string appear difficult to understand.

By identifying each transformation and reversing them systematically, we were able to recover the original flag.

### 🚩 Final Flag

```text
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
```

---

<p align="center">

⭐ <b>picoCTF 2026 — Undo</b> ⭐

<br><br>

<i>Learn • Practice • Break • Understand • Repeat</i>

</p>
