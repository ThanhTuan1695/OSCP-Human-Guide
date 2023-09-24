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
alias iplab='export IP=$IP'

# Misc
alias clab='mkdir $lab && cd'
