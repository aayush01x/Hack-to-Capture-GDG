### Challenge 1: Equation
Use `exiftool` to find the flag hidden in the comment section. The flag format is `CTFlearn{I_Like_Math_x_y}`, where `x` and `y` satisfy the equations:  
- \(3x + 5y = 31\)  
- \(7x + 9y = 59\)  

The solution is \(x = 2\) and \(y = 5\).

**Flag:** `CTFlearn{I_Like_Math_2_5}`

---

### Challenge 2: Corruption?
The correct file signature for a GIF is `"47 49 46 38 39 61"`. The given file signature shows only `"39 61"`, so we need to add the missing bytes. Once fixed, the file contains a Base64-encoded flag:  
`ZmxhZ3tnMWZfb3JfajFmfQ==`

**Flag:** `flag{g1f_or_j1f}`

---

### Challenge 3: Santa's Secrets
Use `binwalk` on the file `3.png` to extract the hidden content. This will recover the original file along with another image, `1.png`, which is an edited version containing noise.


### Challenge 7: Spectrogram Clue

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


### Challenge 8: Communication Lost 2

```bash
# Analyzed the spectrogram but found nothing suspicious.
# Tried other usual techniques, but no significant findings.
```

### Challenge 9: The Wanderer

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

### Challenge 10: Pokemon

```
# Analyzed the spectrogram and noticed a suspicious pattern at the start of the waveform.
# The pattern resembled dots and dashes, indicating Morse code.
# Decoded the pattern using an online Morse code translator, revealing the flag.
```
# Flag
MORSECODEFTW
```