🧩 picoCTF 2026 – Undo
Challenge Description

Challenge: Undo
Category: General Skills
Difficulty: Easy
Platform: picoCTF 2026

Problem

The challenge provides a flag that has undergone a series of Linux text transformations. The goal is to reverse each transformation in the correct order and recover the original flag.

The important part of this challenge is understanding that transformations must be undone in the reverse order in which they were originally applied.

🔍 Solution Approach

The challenge provided the following encoded text:

KXBwMDhxNzdwLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShsenJxbnBu

We need to reverse the transformations step by step.

Step 1 – Reverse Base64 Encoding

The hint indicated:

Hint: Try reversing: base64

Since the original transformation was Base64 encoding, we need to decode it using:

base64 -d
Command
echo "KXBwMDhxNzdwLWZhMDFnQHplMHNmYTRlRy1nazNnLXRhMWZlcmlyRShsenJxbnBu" | base64 -d

This produces:

)pp08q77p-fa01g@ze0sfa4eG-gk3g-ta1ferirE(lzrqnpn
Step 2 – Reverse the Text

The next hint was:

Hint: Reversed the text.

The rev command reverses the characters in a string.

Command
echo ")pp08q77p-fa01g@ze0sfa4eG-gk3g-ta1ferirE(lzrqnpn" | rev

Output:

npnqrzl(Eriref1at-g3kg-Ge4afs0ez@g10af-p77q80pp)
Step 3 – Replace Dashes with Underscores

The challenge indicated:

Hint: Replaced underscores with dashes.

Therefore, we need to reverse this transformation by changing - back to _.

The tr command can perform character substitution.

Command
echo "npnqrzl(Eriref1at-g3kg-Ge4afs0ez@g10af-p77q80pp)" | tr '-' '_'

Output:

npnqrzl(Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp)
Step 4 – Replace Parentheses with Curly Braces

The next transformation was:

Replaced curly braces with parentheses.

So we reverse it by changing:

( → {
) → }
Command
echo "npnqrzl(Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp)" | tr '()' '{}'

Output:

npnqrzl{Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp}
Step 5 – Reverse ROT13

The final transformation was:

Applied ROT13 to letters.

ROT13 is its own inverse, meaning applying ROT13 again restores the original text.

We can use tr:

tr 'A-Za-z' 'N-ZA-Mn-za-m'
Command
echo "npnqrzl{Eriref1at_g3kg_Ge4afs0ez@g10af_p77q80pp}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'

Output:

academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
🚩 Recovered Flag
academy{Revers1ng_t3xt_Tr4nsf0rm@t10ns_c77d80cc}
🧠 Key Concepts Learned

This challenge demonstrates several useful Linux command-line techniques:

Transformation	Reverse Operation	Linux Command
Base64 encoding	Base64 decoding	base64 -d
Text reversal	Reverse characters	rev
_ → -	- → _	tr '-' '_'
{} → ()	() → {}	tr '()' '{}'
ROT13	ROT13 again	tr 'A-Za-z' 'N-ZA-Mn-za-m'
Important Lesson

When reversing a sequence of transformations, start with the last transformation and work backwards.

The complete reverse process was:

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
Original Flag
💻 Commands Used

For a concise command reference:

base64 -d
rev
tr '-' '_'
tr '()' '{}'
tr 'A-Za-z' 'N-ZA-Mn-za-m'
📌 Takeaway

The Undo challenge is a good introduction to Linux text-processing utilities and demonstrates how seemingly complicated encoded data can be recovered by systematically reversing each transformation.

The main commands practiced were base64, rev, and tr, along with the concept of reversing transformations in the correct order.
