# Writeup
### PART 1

## Challenge 1
used
```bash
$ file math.jpg
```
got "The flag is of the form:",this didnt reveal equations so used 

```bash
$ exiftool math.jpg
```
this gave "The flag for this challenge is of the form:..CTFlearn{I_Like_Math_x_y}..where x and y are the solution to these equations:..3x + 5y = 31..7x + 9y = 59..." in comment
solving equations answer is CTFlearn{I_Like_Math_2_5}

## Challenge 3
extracted 2 images 1.png and 3.png from Santa.rar.Then I used 
```bash
$ exiftool 1.png 
$ exiftool 3.png
```
got Trailer data after PNG IEND chunk in warning for 3.png
then used binwalk to extract but didn't get much
```bash 
$ binwalk 3.png
$ binwalk -e 3.png
$ cd _3.png.extracted
$ ls
```
got 4 files here,2 of them of .zlib format.Uncompressed them but did not get anything.
then used zsteg 
```bash 
$ zsteg -a 3.png
```
"[?] 1169169 bytes of extra data after image end (IEND), offset = 0xccb6" got this indicating data attached.
```bash 
$ dd if=3.png bs=1 skip=52406 of=extra_data.bin
$ file extra_data.bin
$ unzip extra_data.bin
```
after this got another image on which "winter is coming" was written.I think this was the flag itself.

## Challenge 7: Spectrogram Clue

```bash
# Step 1: Analyze the zip file
strings message.zip
# Output: seeingisbelieving/help.me

# Step 2: Extract the zip file
unzip message.zip

# Step 3: Navigate to the extracted folder
cd seeingisbelieving/help.me

# Step 4: Analyze the file format
xxd help.me
# Observed: File is an OGG audio file

# Step 5: Rename the file to .ogg
mv help.me help1.ogg

# Step 6: Open the file in Sonic Visualizer
# Add a spectrogram layer to reveal the hidden QR code.

# Step 7: Scan the QR code
# The QR code links to a pastebin URL.

# Flag
the_flag_is{A_sP3c7r0grAm?!}
```


## Challenge 8: Communication Lost 2

```bash
# Analyzed the spectrogram but found nothing suspicious.
# Tried other usual techniques, but no significant findings.
```

## Challenge 9: The Wanderer

```bash
# Used Stegseek to brute force the passphrase for image.jpg
sudo stegseek --crack image.jpg wordlist.txt cracked.txt

# Output:
# [i] Found passphrase: "urahara1"
# [i] Original filename: "flag.txt".
# [i] Extracting to "cracked.txt".

# Flag
0xL4ugh{W4RM_UP_STE94N0_G0OD_J0B}
```

## Challenge 10: Pokemon

```
# Analyzed the spectrogram and noticed a suspicious pattern at the start of the waveform.
# The pattern resembled dots and dashes, indicating Morse code.
# Decoded the pattern using an online Morse code translator, revealing the flag.
```
# Flag
MORSECODEFTW




### PART 2
```bash
# MemLabs Lab 0
volatility -f Challenge.raw imageinfo
volatility -f Challenge.raw --profile=Win7SP1x86 pslist
volatility -f Challenge.raw --profile=Win7SP1x86 cmdscan
# Output: C:\Python27\python.exe C:\Users\hello\Desktop\demon.py.txt
volatility -f Challenge.raw --profile=Win7SP1x86 consoles
volatility -f Challenge.raw --profile=Win7SP1x86 envars
volatility -f Challenge.raw --profile=Win7SP1x86 hashdump
# Flag: flag{you_are_good_but1_4m_b3tt3r}

# MemLabs Lab 1
volatility -f MemoryDump_Lab1.raw imageinfo
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 procdump -p <process-id> --dump-dir <directory>
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 cmdscan
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 console
# Flag: flag{th1s_1s_th3_1st_st4g3!!}

# MemLabs Lab 2
volatility -f MemoryDump_Lab2.raw imageinfo
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 filescan | grep kdbx
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fb112a0 --dump-dir <directory>
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 envars
# Flag: flag{w3lc0m3_T0_$T4g3_!_Of_L4B_2}

# MemLabs Lab 3
volatility -f MemoryDump_Lab3.raw imageinfo
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 pstree
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 cmdline
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 filescan > mem3_filescan.txt
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000003de1b5f0 -D
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000003e727e50 -D
# Flag: inctf{0n3_h4lf_1s_n0t_3n0ugh}

# MemLabs Lab 4
volatility -f MemoryDump_Lab4.raw imageinfo
volatility -f MemoryDump_Lab4.raw --profile=Win7SP1x64 pslist
vol.py -f MemoryDump_Lab4.raw --profile=Win7SP1x64 mftparser > mem4_mft.txt
volatility -f MemoryDump_Lab4.raw --profile=Win7SP1x64 mftparser > mft.txt
# Flag: inctf{1_is_n0t_EQu4l_7o_2_bUt_th1s_d0s3nt_m4ke_s3ns3}

# MemLabs Lab 5
volatility -f MemoryDump_Lab5.raw imageinfo
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 cmdline
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 netscan
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 iehistory
# Flag: flag{!!_w3LL_d0n3_St4g3–1_0f_L4B_5_D0n3_!!}

# MemLabs Lab 6
volatility -f MemoryDump_Lab6.raw imageinfo
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 cmdline
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 filescan > mem6_filescan.txt
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000005fcfc4b0 -D
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 consoles
# Flag: inctf{thi5cH4LL3Ng3_!s_g0nn4_b3_?_aN_Am4zINg_!_i_gU3Ss???}
```


### PART 3
### Exercises and Solutions

**Exercise 001:**  
With the help of image we know the city's name i.e Kiffa. It is told in the tweet that the picture is taken at morning and we can see clearly the Sun is on the left side in the image , so the person taking the image must be facing the south.
If we look carefully we can see that the road is a paved one and also it kind of moves up (like a hill). There are also a bit of trees in the front so we can keep an eye on the map for it. So we are looking for a place with the above
description . I searched for the place in google earth and saw that there are only two south facing roads with some trees in their way , so i was able to find the place after some searching.

#### COORDINATES 16°36'33"N 11°23'52"W ####

**Exercise 002:**  
The flinders street sign makes it very easy to locate the place
#### a) Flinders Street railway station ####
There are two structures which look to be tall one is on the pointy tower on the left of the HWT Building and one is to right (the tall blue one) , after some searching I found that the tower to left is the Melbourne Spire which is 162m tall
whereas the one on the left are the FOCUS apartments which are 167m tall .
#### b) Central Equity's FOCUS Apartments #### 

**Exercise 003:**  
Upon searching about the visit I found out that the visit took place at -
#### Presidential Complex (Tukrey) in Ankara ####
#### COORDINATES - 39°55′51″N 32°47′56″E﻿ #####

**Exercise 004:**  
I searched the image through google lens and found this https://oanresort.wixsite.com/chuuk , which is the website of the resort and has the same image as that given in the challenge.
#### a) Oan Resort #####
#### b) COORDINATES -  7°21'48"N 151°45'20"E ####
I took the help of the two islands behind the resort to check in which direction was the camera facing and i got that the camera was facing
#### c) North - West ####

**Exercise 005:**  
Well first thought which came to mind is to search zoos which are home to polar bears , and also live camera feed not being common was a thing of interest , results showed san diego zoo and after seeing some videos and live cam feed
https://zoo.sandiegozoo.org/cams/polar-cam I was sure that this is the one. With help of the rock and the green roof i was able to find the exact coordinates of the place where the bears were lying and temperature data was available as well.
#### a) San Diego Zoo ####
#### b) TEMPERATURE - ABOUT 15 deg celcius ####
#### c) COORDINATES - 32°44'04"N 117°09'16"W ####
 

**Exercise 006:**  
No, this photo is not correct, as the same image can be found in different places.  

**Exercise 007:**  
Lisbon  
Year: 2019  
Website: [www.tutankamon.pt](http://www.tutankamon.pt)  

**Exercise 008:**  
Shen's Performance  
Date: 7 Jan 2023  
Venue: Chrysler Hall  
