## Challene 5

We were first given a file called megatron.png. Using stegsolvo on the file and changing the plane to red plane 0, we found some text. Namely: "Spectogram" and "Cat! = Rar!"
Using binwalk -M --dd=.* megatron.png, i was able to extract a Rar file called '28E4B'. The Rar contained two file, first a mp3 and next a file called y0u_4r3_cl0s3.rar'.
Using spek purrr_2.mp3, I found a password writted : 'sp3ctrum_1s_y0ur_fr13nd'.
Also the other file appeared to be a data file when file was used, but when opening the file, the first word was Cat!.
Changing Cat! => Rar!, thereby changing the file format the file turned to a Rar archive.
Unarchiving this required a password, using the one found earlier we optain a text file called "f1n4lly.txt".
This file contained a base64 encrypted message which translated to "f0r3n51cs_ma5t3r".