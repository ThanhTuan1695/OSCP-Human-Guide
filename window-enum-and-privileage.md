NOte:

```
Did you remember? now we are in service account called sql_svc. It's good practice to check recently accessed files/executed commands (Keep in mind as good practice).  Mostly (default) our console history will be saved in C:\Users\<account_name>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt .
```
# find the file cgi (Get-ChildItem)
``` 
    cgi c:\\ -Force -r -fi user.txt 2>NULL 
    cgi c:\\ -Force -r -fi *.txt 2>NULL

```
