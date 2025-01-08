# Challenge 5

We are provided with an image megatron.png 

![megatron](https://github.com/user-attachments/assets/8191cfdf-cd60-4962-8fb6-e9ed85e4588b)

```
┌──(kanishk㉿arthur)-[~/Downloads]
└─$ binwalk megatron.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 640 x 448, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
167499        0x28E4B         RAR archive data, version 5.x

                                                                                                                    
```
On extracting the files:

```
┌──(kanishk㉿arthur)-[~/Downloads]
└─$ binwalk --dd='.*' megatron.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 640 x 448, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
167499        0x28E4B         RAR archive data, version 5.x
```
![image](https://github.com/user-attachments/assets/6c902fc2-aac2-41b0-9f9b-53af7376831d)

On extracting the files from 28E4B we get two files:

![image](https://github.com/user-attachments/assets/05f5d902-f8c9-4f47-8477-18ce6edef6d7)

On opening the audio file and analyzing its spectrogram:

![image](https://github.com/user-attachments/assets/b910d3e0-effd-4247-9b44-cc8caba9f5a9)

we get the phrase ``` sp3ctrum_1s_y0ur_fr13nd```

now we will try to extract the rar file:

```
                                                                                                                   
┌──(kanishk㉿arthur)-[~/Downloads/_megatron.png.extracted]
└─$ file y0u_4r3_cl0s3.rar
y0u_4r3_cl0s3.rar: data
```
So the file is actually data so we will try to check is hex data:

```
└─$ xxd y0u_4r3_cl0s3.rar
00000000: 4361 7421 1a07 0100 3392 b5e5 0a01 0506  Cat!....3.......
00000010: 0005 0101 8080 007c bc22 8d58 0203 3c90  .......|.".X..<.
00000020: 0104 c102 2067 b83d 0880 0300 0b66 316e  .... g.=.....f1n
00000030: 346c 6c79 2e74 7874 3001 0003 0f67 c16b  4lly.txt0....g.k
00000040: 5eea ad33 4801 8fe1 06a1 a1b4 9cd8 7130  ^..3H.........q0
00000050: d73e 873b f253 bf05 2444 2af9 7806 4f48  .>.;.S..$D*.x.OH
00000060: 7a08 9021 dcde 2e38 b30a 0302 7d84 a466  z..!...8....}..f
00000070: 0f01 d601 1485 be3b 2d96 5f8c 4f57 4711  .......;-._.OWG.
00000080: b087 2992 f043 d1ee ab9a 4f1a 3408 dc6a  ..)..C....O.4..j
00000090: fd43 2438 9f7c c279 9461 8767 409d 196d  .C$8.|.y.a.g@..m
000000a0: f2b3 4377 9aa9 f326 ba94 fa90 88e7 e1f3  ..Cw...&........
000000b0: 3f4f ca1b 9ccb 4b5f 566b 915a 0f03 7572  ?O....K_Vk.Z..ur
000000c0: 9c39 4967 f1c7 1499 10b4 78cf 6cbb eae9  .9Ig......x.l...
000000d0: 9035 eb88 bcff 9ae3 2d2e eab2 2cdc c281  .5......-...,...
000000e0: 8fde 1db7 a8ab ea0d 8863 8e80 0ee3 1c37  .........c.....7
000000f0: 9205 0565 28b2 cb2b d9fb 67d0 6263 bbe7  ...e(..+..g.bc..
00000100: be57 694a 1d77 5651 0305 0400            .WiJ.wVQ....
```

We will change the header data to 

![image](https://github.com/user-attachments/assets/df0664e9-90a9-4c0f-ab53-cad9eeea7212)

now we can extract the file
```
└─$ unrar x -psp3ctrum_1s_y0ur_fr13nd y0u_4r3_cl0s3.rar

UNRAR 7.10 beta 2 freeware      Copyright (c) 1993-2024 Alexander Roshal


Extracting from y0u_4r3_cl0s3.rar
```
```
└─$ cat f1n4lly.txt   
            __/| 
            \o.O|
       _____(___)______ 
      |       U        |________    __
      |ZjByM241MWNzX21h|        |__|  |_________
      |________________|NXQzcg==|::|  |        /
      |                \._______|::|__|       <
      |                         \::/  \._______\
      |
      |                                                                
```
We get the phrase ZjByM241MWNzX21hNXQzcg=== which on converting from base64 gives:

```f0r3n51cs_ma5t3r```






                                                                                                                    
