# Writeup

## Challenge 7  

### Step 1: Unzipping the File  
```bash
$ unzip message.zip
```  
Extract the contents of `message.zip`.  

### Step 2: Locate the New Folder  
A folder named `seeingisbelieving` appears.  

### Step 3: Change Directory  
Navigate into the `seeingisbelieving` folder.  

### Step 4: List Folder Contents  
Inside, we find a file named `help.me`.  

### Step 5: Check File Type  
```bash
$ file help.me
```  
The `file` command reveals that `help.me` is an `.ogg` audio file.  

### Step 6: Rename the File  
```bash
$ mv help.me help.ogg
```  
Change the file extension to `.ogg` to ensure compatibility with audio tools.  

### Step 7: Analyze the Audio File  
Open the `.ogg` file in Audacity and switch to **Spectrogram View**.  

### Step 8: Extract the Flag  
Upon inspection, a QR code is visible in the spectrogram. Scanning the QR code reveals the flag.  

### Flag  

```txt
the_flag_is{A_sP3c7r0grAm?!}
```  
