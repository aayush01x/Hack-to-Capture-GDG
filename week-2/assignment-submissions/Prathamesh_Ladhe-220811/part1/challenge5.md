## Challenge 5
Using Stegsolve on image using Blue plane 0 , we get

```
Spectogram







Cat!=Rar!
```
- Hint to use Spectogram mode
- Binwalk shows files in the image
- Extracting it , we get a RAR file
- Extracting the rar file we get 2 files - 1) purrr_2.mp3 2)y0u_4r3_cl0s3.rar
- Using the spectogram hint, open the mp3 in audacity with spectogram mode.
- Adjust the height to get the message [(cat symbol)]sp3ctrum_1s_y0ur_fr13nd
- Now extract the second rar, the passphrase is the previous message
- text file is obtained 
- cat f1n4lly.txt
```bash
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
- We obtain the base64 encoded message ZjByM241MWNzX21hNXQzcg==

- decode it to get the flag
```
f0r3n51cs_ma5t3r
```