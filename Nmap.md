
###### Initial scan
```
nmap $IP -Pn -sVC -oN initial -A -vvv
```

###### Full port scan
```
nmap -p --min-rate 10000 -vvv -oN allPorts
```