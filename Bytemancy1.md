### Bytemancy 1 (General Skills)

**What the challenge asked:**
Connect to a remote netcat server and send the ASCII decimal 101 exactly 1751 times, side-by-side with no spaces. The hint explicitly requested using Python instead of copy-pasting.

**The steps and commands I used:**
* **Identifying the payload:** I determined that ASCII decimal 101 corresponds to the lowercase letter 'e'. 
* **Crafting the payload locally:** I used Python's string multiplication `print(chr(101)*1751)` to generate the exact string.
* **Automating delivery with a pipe:** Since the remote server only accepts the raw string and cannot evaluate Python code, I ran the Python command locally and piped (`|`) the standard output directly into the netcat connection before the server even prompted for it:
  `python3 -c "print(chr(101)*1751)" | nc xebec.cylabacademy.net 41986`
* **Result:** The server immediately processed the piped input and returned the flag.

**What I learned:**
* How to use the Linux pipe (`|`) to send the output of a local command as the input to a network connection.
* Why remote netcat prompts (`==>`) cannot execute code, and why payloads must be evaluated locally before transmission.

**Flag:** `academy{h0w_m4ny_e's???_17ac1ce5}`
**Date:** November 10, 2026
