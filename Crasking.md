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


## ZIP cracking
```bash
john-the-ripper.zip2john backup.zip > backup.hash

Created directory: /home/splitunknown/snap/john-the-ripper/581/.john
Created directory: /home/splitunknown/snap/john-the-ripper/581/.john/opencl
ver 2.0 efh 5455 efh 7875 backup.zip/source_code.php PKZIP Encr: TS_chk, cmplen=554, decmplen=1211, crc=69DC82F3 ts=2297 cs=2297 type=8
```

output:- 
```bash
cat backup.hash 
backup.zip/source_code.php:$pkzip$1*1*2*0*22a*4bb*69dc82f3*0*49*8*22a*2297*8e9e8de3a4b82cc98077a470ef800ed60ec6e205dc091547387432378de4c26ae8d64051a19d86bff2247f62dc1224ee79f048927d372bc6a45c0f21753a7b6beecfa0c847126d88084e57ddb9c90e9b0ef8018845c7d82b97b438a0a76e9a39c4846a146ae06efe4027f733ab63b509a56e2dec4c1dbce84337f0816421790246c983540c6fab21dd43aeda16d91addc5845dd18a05352ca9f4fcb45f0135be428c84dbac5a8d0c1fb2e84a7151ec3c1ae9740a84f2979d79da2e20d4854ef4483356cd078099725b5e7cf475144b22c64464a85edb8984cf7fc41d6a177f172c65e57f064700b6d49ef8298d83f42145e69befeab92453bd5f89bf827cd7993c9497eb2ad9868abd34b7a7b85f8e67404e2085de966e1460ad0ea031f895c7da70edbe7b7d6641dcdf6a4a31abc8781292a57b047a1cc5ce5ab4f375acf9a2ff4cac0075aa49e92f2d22e779bf3d9eacd2e1beffef894bc67de7235db962c80bbd3e3b54a14512a47841140e162184ca5d5d0ba013c1eaaa3220d82a53959a3e7d94fb5fa3ef3dfc049bdbd186851a1e7a8f344772155e569a5fa12659f482f4591198178600bb1290324b669d645dbb40dad2e52bf2adc2a55483837a5fc847f5ff0298fd47b139ce2d87915d688f09d8d167470db22bda770ce1602d6d2681b3973c5aac3b03258900d9e2cc50b8cea614d81bcfbb05d510638816743d125a0dce3459c29c996a5fdc66476f1b4280ac3f4f28ed1dbff48ef9f24fc028acc1393d07233d0181a6e3*$/pkzip$:source_code.php:backup.zip::backup.zip
```

cracking
```bash
john-the-ripper --wordlist=/home/splitunknown/Tools/SecLists/Passwords/Leaked-Databases/rockyou.txt backup.hash 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 16 OpenMP threads
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
pass1word        (backup.zip/source_code.php)     
1g 0:00:00:00 DONE (2023-09-19 20:37) 33.33g/s 1092Kp/s 1092Kc/s 1092KC/s 123456..dyesebel
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```
