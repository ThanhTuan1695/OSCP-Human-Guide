# Nmap scan
Not shown: 994 closed tcp ports (conn-refused)                                                                                       
PORT     STATE SERVICE    VERSION                                                                                                    
21/tcp   open  ftp        pyftpdlib 1.5.6                                                                                            
| ftp-syst:                                                                                                                          
|   STAT:                                                                                                                            
| FTP server status:                                                                                                                 
|  Connected to: 192.168.173.72:21                                                                                                   
|  Waiting for username.                                                                                                             
|  TYPE: ASCII; STRUcture: File; MODE: Stream                                                                                        
|  Data connection closed.                                                                                                           
|_End of status.                                                                                                                     
22/tcp   open  ssh        OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)                                                             
| ssh-hostkey:                                                                                                                       
|   2048 5b:a7:37:fd:55:6c:f8:ea:03:f5:10:bc:94:32:07:18 (RSA)                                                                       
|   256 ab:da:6a:6f:97:3f:b2:70:3e:6c:2b:4b:0c:b7:f6:4c (ECDSA)                                                                      
|_  256 ae:29:d4:e3:46:a1:b1:52:27:83:8f:8f:b0:c4:36:d1 (ED25519)                                                                    
25/tcp   open  smtp       Exim smtpd                                                                                                 
| smtp-commands: solstice Hello nmap.scanme.org [192.168.45.171], SIZE 52428800, 8BITMIME, PIPELINING, CHUNKING, PRDR, HELP          
|_ Commands supported: AUTH HELO EHLO MAIL RCPT DATA BDAT NOOP QUIT RSET HELP                                                        
80/tcp   open  http       Apache httpd 2.4.38 ((Debian))                                                                             
|_http-server-header: Apache/2.4.38 (Debian)                                                                                         
|_http-title: Site doesn't have a title (text/html).                                                                                 
2121/tcp open  ftp        pyftpdlib 1.5.6                                                                                            
| ftp-anon: Anonymous FTP login allowed (FTP code 230)                                                                               
|_drws------   2 www-data www-data     4096 Jun 18  2020 pub                                                                         
| ftp-syst:                                                                                                                          
|   STAT:                                                                                                                            
| FTP server status:                                                                                                                 
|  Connected to: 192.168.173.72:2121                                                                                                 
|  Waiting for username.                                                                                                             
|  TYPE: ASCII; STRUcture: File; MODE: Stream                                                                                        
|  Data connection closed.                                                                                                           
|_End of status.                                                                                                                     
3128/tcp open  http-proxy Squid http proxy 4.6                                                                                       
|_http-server-header: squid/4.6                                                                                                      
|_http-title: ERROR: The requested URL could not be retrieved                                                                        
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel                                                                              

# Enum
## port 21

version: pyftpdlib 1.5.6 

Search: 
- windows/local/37197.py

## port 22
version: OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
## port 25

Exim smtpd

## port 80
apache 2.4.38

## Port 2121
ftp-anon: Anonymous FTP login allowed (FTP code 230)                                                                               
|_drws------   2 www-data www-data     4096 Jun 18  2020 pub  

## port 3128
_http-server-header: squid/4.6                        
