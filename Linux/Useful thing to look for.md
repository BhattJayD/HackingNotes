#### passwd

```bash
investigator@10.10.224.80:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
```

#### Identifying Groups

```bash
investigator@10.10.224.80:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,ubuntu,investigator
```

To determine which groups a specific user is a member of, we can run the following command:
```bash
investigator@ip-10-10-224-80:~$ groups sys
sys : sys
investigator@ip-10-10-224-80:~$ groups investigator
investigator : investigator adm dialout cdrom floppy sudo audio dip video plugdev netdev lxd
investigator@ip-10-10-224-80:~$ groups bob
bob : bob
investigator@ip-10-10-224-80:~$ groups root
root : root
investigator@ip-10-10-224-80:~$ 
```

Alternatively, to list all of the members of a specific group, we can run the following command:

```bash
investigator@10.10.224.80:~$ getent group adm 
adm:x:4:syslog,ubuntu,investigator
```

```bash
investigator@10.10.224.80:~$ getent group 27 
sudo:x:27:ubuntu,investigator
```


#### User Logins and Activity
```bash
investigator@10.10.224.80:~$ last
investig pts/1        10.10.152.206    Tue Feb 13 02:37   still logged in
investig pts/0        10.10.101.34     Tue Feb 13 02:29   still logged in
reboot   system boot  5.4.0-1029-aws   Tue Feb 13 02:28   still running
investig pts/1        10.10.101.34     Tue Feb 13 02:23 - crash  (00:05)
investig pts/0        10.10.101.34     Tue Feb 13 02:16 - 02:22  (00:05)
reboot   system boot  5.4.0-1029-aws   Tue Feb 13 02:14   still running
```

```bash
investigator@10.10.224.80:~$ lastlog
Username         Port     From             Latest
root                                       **Never logged in**
daemon                                     **Never logged in**
bin                                        **Never logged in**
sys                                        **Never logged in**
sync                                       **Never logged in**
```

#### find stat of file
```
investigator@ip-10-10-224-80:~$ sudo stat /home/jane/.ssh/authorized_keys 
  File: /home/jane/.ssh/authorized_keys
  Size: 1136      Blocks: 8          IO Block: 4096   regular file
Device: ca01h/51713dInode: 257561      Links: 1
Access: (0666/-rw-rw-rw-)  Uid: ( 1002/    jane)   Gid: ( 1002/    jane)
Access: 2024-02-13 00:34:53.692530853 +0000
Modify: 2024-02-13 00:34:16.005897449 +0000
Change: 2024-02-13 00:34:16.005897449 +0000
 Birth: -
investigator@ip-10-10-224-80:~$ 
```

#### debsums

```bash
investigator@ip-10-10-224-80:~$ sudo debsums -e -s
debsums: changed file /etc/sudoers (from sudo package)
```
we provide the `-e` flag to only perform a configuration file check. In addition, we provide the `-s` flag to silence any error output that may fill the screen.

#### Chkrootkit

```bash
investigator@10.10.224.80:~$ sudo chkrootkit
ROOTDIR is `/'
Checking `amd'...                                           not found
Checking `basename'...                                      not infected
Checking `biff'...                                          not found
Checking `chfn'...                                          not infected
Checking `chsh'...                                          not infected
Checking `cron'...                                          not infected
Checking `crontab'...                                       not infected
Checking `date'...                                          not infected
```

#### RKHunter

```bash
investigator@10.10.224.80:~$ sudo rkhunter -c -sk
[ Rootkit Hunter version 1.4.6 ]

Checking system commands...

  Performing 'strings' command checks
    Checking 'strings' command                               [ OK ]

  Performing 'shared libraries' checks
    Checking for preloading variables                        [ None found ]
```


#### Check loggedin shell or Display All Processes in a Hierarchical Tree with ps Command

```bash
ps -eaf --forest
```

output:- 

```bash
root       822     1  0 13:16 ?        00:00:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
root       843     1  0 13:16 ttyS0    00:00:00 /sbin/agetty -o -p -- \u --keep-baud 115200,38400,9600 ttyS0 vt220
root       848     1  0 13:16 ?        00:00:00 /usr/sbin/sshd -D
root      1549   848  0 13:31 ?        00:00:00  \_ sshd: magna [priv]
magna     1668  1549  0 13:32 ?        00:00:00      \_ sshd: magna@pts/0
magna     1676  1668  0 13:32 pts/0    00:00:00          \_ -bash
magna     1764  1676  0 13:35 pts/0    00:00:00              \_ ps -eaf --forest
root       849     1  0 13:16 tty1     00:00:00 /sbin/agetty -o -p -- \u --noclear tty1 linux
```
