SSH id_rsa
```
wget https://raw.githubusercontent.com/openwall/john/bleeding-jumbo/run/ssh2john.py
python3 ssh2john.py matt_key > matt_hash
```

now crack with john

```
john-the-ripper --wordlist=/home/splitunknown/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt matt_hash
```

output 
```
Warning: detected hash type "SSH", but the string is also recognized as "ssh-opencl"
Use the "--format=ssh-opencl" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 1 for all loaded hashes
Cost 2 (iteration count) is 2 for all loaded hashes
Will run 16 OpenMP threads
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
computer2008     (matt_key)     
1g 0:00:00:00 DONE (2023-02-12 13:52) 8.333g/s 2057Kp/s 2057Kc/s 2057KC/s confused23..clowee
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```
view output
```
$john-the-ripper --show matt_hash 
matt_key:computer2008
1 password hash cracked, 0 left
```



## HashCat

hash identify from here

```
https://hashcat.net/wiki/doku.php?id=example_hashes
```
EG:- ``$1$ 500

```
hashcat -m 500 m4lwhere ~/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt
```