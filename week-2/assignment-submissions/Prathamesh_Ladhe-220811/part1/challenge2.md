
## Challenge 2

```bash 
$ xxd unopenable.gif | head -n 20
00000000: 3961 f401 f401 f400 0000 0000 3a00 0000  9a..........:...
00000010: 003a 3a00 3a66 0000 6600 3a00 0066 903a  .::.:f..f.:..f.:
00000020: 0090 3a3a b666 00b6 663a 9090 3adb 903a  ..::.f..f:..:..:
00000030: ffb6 6600 3a90 663a 9000 6690 0066 b63a  ..f.:.f:..f..f.:
00000040: 66b6 9066 903a 90db 66b6 ffb6 ffb6 ffdb  f..f.:..f.......
00000050: 90ff ffb6 90db ffb6 ffff ffff dbdb ffff  ................
00000060: ffff ff00 0000 0000 0021 f904 080a 0000  .........!......
00000070: 0021 ff0b 4e45 5453 4341 5045 322e 3003  .!..NETSCAPE2.0.
00000080: 0100 0000 21ff 0b49 6d61 6765 4d61 6769  ....!..ImageMagi
00000090: 636b 0d67 616d 6d61 3d30 2e34 3534 3535  ck.gamma=0.45455
000000a0: 002c 0000 0000 f401 f401 0005 fe60 278e  .,...........`'.
000000b0: 6469 9e68 aaae 6ceb be70 2ccf 746d df78  di.h..l..p,.tm.x
000000c0: aeef 7cef ffc0 a070 482c 1a8f c8a4 72c9  ..|....pH,....r.
000000d0: 6c3a 9fd0 a874 4aad 5aaf d8ac 76cb ed7a  l:...tJ.Z...v..z
000000e0: bfe0 b078 4c2e 9bcf e8b4 7acd 6ebb dff0  ...xL.....z.n...
000000f0: b87c 4eaf dbef f8bc 7ecf effb ff80 8182  .|N.....~.......
00000100: 8384 8586 8788 898a 8b8c 8d8e 8f90 9192  ................
00000110: 9394 9596 9798 999a 9b9c 9d9e 9fa0 a1a2  ................
00000120: a3a4 a5a6 a7a8 a9aa abac adae afb0 b1b2  ................
00000130: b3b4 b5b6 b7b8 b9ba bbbc bdbe bfc0 c1c2  ................
```

```bash
echo -n -e '\x47\x49\x46\x38' > header.bin
cat header.bin unopenabe.gif > repaired.gif
```

- 9a suggested that the header is incomplete and it should've been GIF89a.
- Added 47 49 46 38 to the start of the hex of the file 
- Got the GIF 
- Decoded the base64 "ZmxhZ3tnMWZfb3JfajFmfQ=="
- The flag flag{g1f_or_j1f}


Hence the flag 

```
flag{g1f_or_j1f}
```
