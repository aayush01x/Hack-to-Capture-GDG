File signature of a GIF file should be GIF87a or GIF89a. 

Use xxd to see that none of them is present.


```
xxd unopenable.gif | head
```


Use a hex editor to change the File signature to GIF89a (as 9a is already present). Save the file to see that this now becomes an openable gif. Extract the Base64 data to get the flag.

Flag - flag{g1f_or_j1f}