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

