# PicoCTF Writeup: n0s4n1ty 1

## Category: Web / Privilege Escalation  
**Tags:** `webshell`, `sudo`, `priv-esc`, `directory traversal`, `flag access`

---

### Challenge Summary

This challenge involved uploading a PHP webshell to gain remote code execution, checking sudo permissions to escalate privileges, and navigating the filesystem to locate and read the flag.

---

### Steps and Explanation

#### Step 1: Upload `C99.php` Webshell

I uploaded `C99.php`, a PHP webshell that provides a web interface to execute commands and browse the server's file system.

> **Reason:**  
> Uploading a webshell is a common technique to gain shell access on a vulnerable web server after exploiting file upload vulnerabilities.

---

#### Step 2: Enumerate Sudo Permissions

I ran:

```bash
sudo -l
````

to list the commands the current user can run with sudo without a password.

> **Reason:**
> This helps identify potential privilege escalation vectors if the user can run commands as root.

---

#### Step 3: Explore Filesystem and Find the Flag

Using the webshell, I explored directories and switched between them to locate where the flag might be stored.

---

#### Step 4: Escalate Privileges and Read the Flag

I used the sudo permission to run the following command as root:

```bash
sudo bash -c 'cd ../../../../../ && ls -la && cd /root && ls -la && cat flag.txt'
```

* `cd ../../../../../` moves up the directory tree to root (`/`).
* `ls -la` lists files in the root directory for inspection.
* `cd /root` changes directory to the root user's home folder.
* `cat flag.txt` outputs the flag content.

> **Reason:**
> The command uses `sudo` to bypass permission restrictions and read the flag file stored in root's home directory.

---

### Conclusion

By uploading a webshell, enumerating sudo permissions, and executing commands with root privileges, I successfully retrieved the flag.

---

**Flag:**
*(Include the actual flag here if allowed by the CTF rules)*
