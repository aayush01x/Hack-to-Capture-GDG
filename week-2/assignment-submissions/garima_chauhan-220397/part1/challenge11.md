flag: fastctf{the hashcat goes meow}

```bash
$ file secret_file
```

this showed it to be a 7zip compressed file. but while extracting through 7z missing a password.

used 7ztojohn and hashcat to crack the password

```bash
$ mv secret_file secret_file.7z
$ /usr/share/john/7z2john.pl secret_file.7z > hash.txt
```

after removing the filename from hash.txt used hashcat
```bash
$ hashcat -m 11600 hash.txt /usr/share/wordlists/rockyou.txt
$ hashcat hash.txt --show
```

password: 12345abc

```bash
$ 7z e secret_file.7z
$ cat flag\ \(81\).txt
```

this had an html file. opened the html file and then used a base64 to bmp file decoder to get the image with the flag