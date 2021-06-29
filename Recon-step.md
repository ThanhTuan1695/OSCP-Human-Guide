# Port scan

nmap -p ip

# quich scan

nmap -sS IP

# standarn namp scan

nmap -sC -sC -vv -A 
nmap -sC -sV -Pn ip

# Fast simple scan
nmap -sS 10.11.1.111

# Full complete slow scan with output
nmap -v -sT -A -T4 -p- -Pn --script vuln -oA full 10.11.1.111

# Autorecon
python3 autorecon.py 10.11.1.111

#rust-scan

rustscan -a 10.10.24.224 -- -sC -sV -oA nmap1
