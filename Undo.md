### Undo (General Skills)

**What the challenge asked:**
The goal was to connect to a remote server using `netcat` and reverse a series of five unknown text transformations step-by-step to recover the original flag. 

**The steps and commands I used:**
* **Getting connected:** I started by pasting the provided netcat command, but it threw a `Name or service not known` error. I realized there was a typo in the domain name. Once I fixed it, `nc chatelaine.cylabacademy.net 24435` got me in.
* **Step 1 (Base64 encoded):** The first string was clearly Base64. My instinct was to pipe it like I normally would in Linux (`echo "string" | base64 -d`), but the server kept rejecting it. I realized the challenge script was already holding the string in memory, so I just needed to pass the raw command: `base64 -d`.
* **Step 2 (Reversed text):** The hint said the text was reversed. I tried things like `rev base64`, but the server complained that `rev takes no arguments` in this environment. I backed off and just typed `rev`, which worked perfectly.
* **Step 3 (Replaced underscores with dashes):** I needed to swap dashes back to underscores. I used the translate command for this: `tr '-' '_'`.
* **Step 4 (Replaced curly braces with parentheses):** Same logic as the previous step, just mapping different characters: `tr '()' '{}'`.
* **Step 5 (Applied ROT13 to letters):** I had to google how to do ROT13 natively in Linux without downloading an external tool. I found out you can actually use `tr` for this by feeding it two alphabet ranges shifted by 13 letters: `tr 'A-Za-z' 'N-ZA-Mn-za-m'`.
* **Result:** `academy{REDACTED}`

**What I learned:**
* Always check for typos in the hostname if `nc` fails to connect.
* Interactive CTF scripts have their own quirks. You don't always need to build a full pipeline with `echo` or pipes (`|`); sometimes they just want the base utility and its flag.
* The `tr` command is way more powerful than I thought. I didn't realize you could use it to solve full ciphers like ROT13 just by shifting the character arrays.

**Date:** November 10, 2026
