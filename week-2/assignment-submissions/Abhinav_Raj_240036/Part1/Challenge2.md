#
used  ```xxd unopenable.gif``` to find the sign signature as 9a. Got to relate it with GIF89a  
Used hexedit to change the initial file signatures to ```47 49 46 38 3 61 f4 01 f4 01```
exported the file named it as un.gif  
Got to see incorrect LSW compression in the image viewer  
Used ```convert un.gif fixed.png
convert fixed.png fixed.gif```
Got 4 images with wwritten ```ZmxhZ3tnMWZfb3JfajFmfQ==``` and decode it. The cipher is base64 encoded as it has == in last.  
The flag is: flag{g1f_or_j1f}
  
