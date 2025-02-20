## Sub domain discovery with ffuf and wfuzz

```bash
ffuf -u https://abc.com/ -w list.txt -H "Host: FUZZ.abc.com" -mc all 
```

Note:-
there is not http:// or https:// in host header


With WFUZZ

```bash
wfuzz -u http://horizontall.htb -w ~/Tools/SecLists/Discovery/DNS/subdomains-top1million-20000.txt -H "Host: FUZZ.horizontall.htb" --hh 194
```



## FUZZING with Request file

```http
POST /administrator HTTP/1.1
Host: 10.10.4.98:8080
Content-Length: 41
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://10.10.4.98:8080
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.6261.112 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://10.10.4.98:8080/administrator
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Connection: close

username=clocky_user&password=FUZZ
```


```bash
ffuf -request req -request-proto http -w ~/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt
```

Note:-  -request-proto use to change protocol default is https

fuzz through some proxy
```bash
ffuf -request req -request-proto http -w ~/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt -x http://127.0.0.1:8081
```

Follow redirect 

-r is use for Follow redirects default is set to false

```bash
ffuf -request req -request-proto http -w ~/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt -x http://127.0.0.1:8081 -r
```


### FUZZING wordpress with WPScan

```bash
sudo docker run -it --rm wpscanteam/wpscan --url http://www.smol.thm/wordpress --disable-tls-checks   --api-token  $wp_token --enumerate u,p,t,tt,cb,dbe
```

To fix network related issue add ``--add-host=www.smol.thm:10.10.169.82`` in your docker command

```bash
sudo docker run -it --rm --add-host=www.smol.thm:10.10.169.82 wpscanteam/wpscan --url http://www.smol.thm/ --disable-tls-checks   --api-token  $wp_token --enumerate u,p,t,tt,cb,dbe  
```

#### wpscan Brute force
```bash
sudo docker run -it --rm -v /home/sh/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt:/rockyou.txt wpscanteam/wpscan --url http://10.10.94.0/wordpress/ --disable-tls-checks -U admin,bob -P /rockyou.txt
```
