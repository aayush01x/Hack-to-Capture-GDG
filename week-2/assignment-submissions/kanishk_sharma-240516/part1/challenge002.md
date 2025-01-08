# Challenge 2

```
└─$ file unopenable.gif   
unopenable.gif: data
```
We find that the file is corrupted
```
$ xxd unopenable.gif |head
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
```
We need to add _47 49 46 38_ to header 

On reading the GIF frame by frame we get the string ```ZmxhZ3tnMWZfb3JfajFmfQ==```
On converting from base64, we get the flag:
```flag{g1f_or_j1f}```
