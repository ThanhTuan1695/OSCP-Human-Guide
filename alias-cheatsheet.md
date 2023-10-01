# config in .zshrc

for conf in "$HOME/.config/zsh/config.d/"*.zsh; do
  source "${conf}"
done

#  alilas openvpn
alias pg='cd ~/Desktop/play-ground && tmux'
alias thm='cd ~/Desktop/thm && tmux'
alias htb='cd ~/Desktop/htb && tmux'
alias ovpn='sudo openvpn ./o.ovpn'

# alias nmap
alias Tnmap='nmap -sC -sV -Pn $IP -o tcp.txt'
alias Unmap='sudo nmap -sU -Pn -p- $IP  -o udp.txt'
alias Fnmap='nmap -v -sT -A -T4 -p- -Pn --script vuln -oA full  $IP'

# nmap automator
alias All='sudo /bin/bash ~/Desktop/nmapAutomator.sh -H $IP -t All -o $lab'
alias autoRe='sudo /bin/bash ~/Desktop/nmapAutomator.sh -H $IP -t '

# smb recon
alias smbNmap='nmap --script=smb-enum* --script-args=unsafe=1 -T5 $IP'
 
# gobuster
alias MFuzz='gobuster dir --url http://$IP -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50'

# share tmux
alias setip='tmux setenv IP $IP'

# Misc
alias clab='mkdir $lab && cd'

# python server 
alias httpgo='python3 -m http.server 9999'

# Port 21
alias nmap21='nmap --script ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 $IP'

# Port 25

alias nmap25='nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 $IP'


