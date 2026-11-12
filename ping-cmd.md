### ping-cmd (General Skills)

**What the challenge asked:**
Connect to a remote server via netcat that provides a ping service, specifically restricted to pinging `8.8.8.8`. The goal was to bypass this restriction and execute arbitrary code to reveal the server's hidden files.

**The steps and commands I used:**
* **Identifying the vulnerability:** The server uses a backend shell command to execute the ping. Because it doesn't sanitize user input, it is vulnerable to command injection.
* **Exploring the directory:** I used the Linux command separator `;` to append an `ls` command immediately after the allowed IP address.
  * Input: `8.8.8.8; ls`
  * This successfully executed the ping, followed by listing the contents of the current directory, revealing the hidden flag file.
* **Extracting the flag:** I ran the connection again, this time injecting a `cat` command to read the discovered file.
  * Input: `8.8.8.8; cat [filename]`

**What I learned:**
* How command injection works when backend scripts fail to sanitize user input.
* How to use shell operators like `;` and `&&` to chain and execute arbitrary commands on a remote target.

**Flag:** `academy{[insert_flag_here]}`
**Date:** November 13, 2026
