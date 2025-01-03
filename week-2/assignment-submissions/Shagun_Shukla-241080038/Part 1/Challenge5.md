# Writeup

## Challenge 5
Used binwalk on megatron.png
```bash
$ binwalk --dd=".*"  megatron.png
```
We found a rar file and opened it with the unarchiver.
It had two files .rar file and .mp3 file.

Checked the .mp3 file's spectrogram and found a string as **sp3ctrum_1s_y0ur_fr13nd**

Used xxd on the rar file since it wasn't opening to check the file signature.
```bash
$ xxd y0u_4r3_cl0s3.rar | head
```
Fixed the signature from Hexed.it.

Got a encoded string in the file as ZjByM241MWNzX21hNXQzcg==

The Flag for the level is ** f0r3n51cs_ma5t3r **.
