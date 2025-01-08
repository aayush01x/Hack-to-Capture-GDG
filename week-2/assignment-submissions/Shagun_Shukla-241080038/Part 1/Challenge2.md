# Writeup

Used exiftool on unopenable.gif which gave a file format error.

Used xxd to see the file signature for unopenable.gif
```bash
$ xxd unopenable.gif
```
The magic numbers only gave 9a and not gif so checked for file signature of gif found the initial magic numbers were deleted.
Used Hexed.it to add 4749 4638 to the file signature of unopenable.gif to a valid gif of 89a version.
The gif had base64 encrypted message as ZmxhZ3tnMWZfb3JfajFmfQ==

Decoded it and found the flag as flag{g1f_or_j1f}
