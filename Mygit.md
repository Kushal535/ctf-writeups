### My Git (General Skills)

**What the challenge asked:**
Clone a custom Git repository, create a `flag.txt` file, and push it back to the server. The catch: the server would only release the flag if the commit was authored exactly by `root:root@academy`.

**The steps and commands I used:**
* **Cloning the repo:** I started by cloning the provided SSH repository using `git clone ssh://git@xebec.cylabacademy.net:206600/git/challenge.git`.
* **Spoofing my identity:** To meet the server's requirement, I changed my local Git configuration to impersonate the root user before making any commits:
  `git config --global user.name root`
  `git config --global user.email root@academy`
* **Creating the payload:** I moved into the directory (`cd challenge`), created the required file (`echo "give me the flag" > flag.txt`), staged it (`git add flag.txt`), and committed it.
* **Handling instance timeouts:** When I tried to push, the connection was refused because my CTF instance had expired. Instead of starting over, I spun up a new instance, grabbed the new port number, and updated my existing repository's remote URL: 
  `git remote set-url origin ssh://git@chatelaine.cylabacademy.net:41348/git/challenge.git`
* **Capturing the flag:** I pushed the commit (`git push`), accepted the SSH fingerprint, entered the instance password, and the server verified my spoofed author identity, returning the flag.
* **Result:** `academy{REDACTED}`

**What I learned:**
* How Git locally tracks author identity and how trivially it can be modified using `git config user.name` and `user.email`. 
* How to fix a broken remote connection using `git remote set-url` without needing to re-clone or rebuild a local repository from scratch.
* Always double-check SSH hostnames for typos when manually typing URLs.

**Date:** November 10, 2026
