# Port scan

nmap -p ip

# quich scan

nmap 

# Fast simple scan
nmap -sS 10.11.1.111

# Full complete slow scan with output
nmap -v -sT -A -T4 -p- -Pn --script vuln -oA full 10.11.1.111

# Autorecon
python3 autorecon.py 10.11.1.111
