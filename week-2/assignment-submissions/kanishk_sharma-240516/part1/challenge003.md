# Challenge 3

```
└─$ unrar x Santa.rar 

UNRAR 7.10 beta 2 freeware      Copyright (c) 1993-2024 Alexander Roshal


Extracting from Santa.rar

Extracting  3.png                                                     OK 
Extracting  1.png                                                     OK 
All OK
```
Now on extracting files from 3.png:
```
└─$ binwalk 3.png                 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 1200 x 875, 8-bit/color RGBA, non-interlaced
78            0x4E            Zlib compressed data, default compression
52406         0xCCB6          PNG image, 1280 x 720, 8-bit/color RGBA, non-interlaced
52447         0xCCDF          Zlib compressed data, compressed

└─$ binwalk --dd='.*' 3.png       

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 1200 x 875, 8-bit/color RGBA, non-interlaced
78            0x4E            Zlib compressed data, default compression
52406         0xCCB6          PNG image, 1280 x 720, 8-bit/color RGBA, non-interlaced
52447         0xCCDF          Zlib compressed data, compressed
```

on using stegsolve and combining 1.png and image we got from binwalk, we get:

![solved](https://github.com/user-attachments/assets/ee5529aa-3e8f-412f-a170-a72397c3f0da)

So, the flag is:
```CTFlearn{Santa_1s_C0ming}```



                                                                                              

