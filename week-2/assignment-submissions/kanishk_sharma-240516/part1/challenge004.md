# Challenge 4

The audio file does not open in audacity as it may be corrupted. So, we change the hex data of the audio file.
```
└─$ xxd newsong.m4a      
00000000: 2020 2020 6669 6c65 7479 7065 4d34 4120      filetypeM4A 
00000010: 0000 0000 4d34 4120 6d70 3432 6973 6f6d  ....M4A mp42isom
00000020: 0000 0000 0000 12ed 6d6f 6f76 0000 006c  ........moov...l
00000030: 6d76 6864 0000 0000 d51b d933 d51b d934  mvhd.......3...4
00000040: 0000 ac44 0006 6800 0001 0000 0100 0000  ...D..h.........
00000050: 0000 0000 0000 0000 0001 0000 0000 0000  ................
00000060: 0000 0000 0000 0000 0001 0000 0000 0000  ................
00000070: 0000 0000 0000 0000 4000 0000 0000 0000  ........@.......
00000080: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000090: 0000 0000 0000 0002 0000 0875 7472 616b  ...........utrak
000000a0: 0000 005c 746b 6864 0000 0007 d51b d933  ...\tkhd.......3
```
On changing the hex data:

![image](https://github.com/user-attachments/assets/7601d666-bf1e-464c-b240-24ee2be8ce42)

We can hear the audio file now and we get the flag as:
```1_c4n_f1x_it```
