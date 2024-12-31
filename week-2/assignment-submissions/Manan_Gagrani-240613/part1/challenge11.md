Checking the filetype, we find that it is a 7zip archive. So rename it to secret_file.7z.

Extracting it needs a password which can be cracked using JohnTheRipper.

Password - 12345abc

The text file contains a base64 string which when converted to an image, gives the flag.

Flag - fastctf{the hashcat goes meow}