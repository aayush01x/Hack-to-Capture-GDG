# 
changed the extension to .7z  
used john to crack the password  
```
./7z2john.pl secret.7z > hash.txt
```
```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```  
Got password as :12345abc   
Got a base64 string in thefile extracted 
Used base64 to image tool to get the flag  
The flag : fastctf{the hashcat goes meow}
