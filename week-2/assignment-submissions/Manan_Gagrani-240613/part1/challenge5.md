Using stegsolve on megatron.png gives hints about using spectrograms and something like Cat! = Rar!

Using binwalk on megatron.png, we get a rar archive. So we extract the rar archive and its data.


```
binwalk --dd=".*" megatron.png
```



```
rar e 28E4B
```


You get two files. A rar archive and a mp3 file.

The rar archive is empty. Checking its hex dump shows that the File signature is incorrect. Given that a hint was given earlier about this, changing the Rar! to Cat! in the hex dump reveals a txt file in the rar archive. But it needs some password to open.


```
xxd y0u_4r3_cl0s3.rar
```


Using exiftool on the mp3 gives a hint that a password is hidden in it. Given that a spectrogram hint was given, analyze the spectrogram of the mp3 to get a password for the rar archive.


```
exiftool purrr_2.mp3
```


Password: sp3ctrum_1s_y0ur_fr13nd

The txt file reveals a base64 string. Decoding it, we get our flag.

Flag - f0r3n51cs_ma5t3r