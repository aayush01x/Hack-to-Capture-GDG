# MemLabs Lab-5 – Writeup

We begin by downloading the memory dump provided in the lab description and renaming it as `lab5.raw` for easier reference.

---

## Initializing the Memory Dump

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:

```bash
volatility -f lab5.raw imageinfo  
```

The output provides various data points about the image, including seven suggested service profiles. One of these profiles must be chosen for subsequent commands.

We select the first profile (`Win7SP1x64`). If any issues arise during the process, we can switch to the other profiles later.

---

## Using Basic Plugins

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).

```bash
volatility -f lab5.raw --profile=Win7SP1x64 pslist  
```

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, a few suspicious processes stand out:

- `NOTEPAD.exe`
- `notepad.exe`  
- `winRAR.exe`

The difference in case between `NOTEPAD.exe` and `notepad.exe` is unusual and worth investigating. The presence of `winRAR.exe` is also notable.

---

## Digging into Processes

To investigate further, we attempt to retrieve the arguments passed to these processes. This can reveal file paths or commands that may provide more context about the process.

```bash
volatility -f lab5.raw --profile=Win7SP1x64 cmdline  
```

```bash
volatility -f lab5.raw --profile=Win7SP1x64 getsids -p <pid>  
```

Upon examination, we find that the file `SW1wb3J0YW50.rar` is associated with the `winRAR.exe` process. The unusual naming suggests a potential base64 encoding, aligning with the lab description's emphasis on suspicious file names.

Additionally, `NOTEPAD.exe` (in uppercase) is being executed from the `Windows` folder, which is highly irregular, indicating potential malware.

---

## Extracting the RAR File

We locate and extract the RAR file using the following commands (address for the RAR file: `0x000000003eed56f0`):

```bash
volatility -f lab5.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003eed56f0 -D .  
```

We rename it to `file.rar` and attempt to extract it using `unrar`:

```bash
unrar e file.rar  
```

At this point, a password is required for `Stage2.png`, but we do not yet have the `Stage1` flag, which is necessary to proceed. We defer extraction until the `Stage1` flag is recovered.

---

## Examining NOTEPAD.exe

We locate files named `notepad.exe` using `filescan` and `grep`:

```bash
volatility -f lab5.raw --profile=Win7SP1x64 filescan | grep -i 'notepad.exe'  
```

The uppercase `NOTEPAD.exe` is found in the `Videos` directory at address `0x000000003ee8d070`.

We extract all files at this location:

```bash
volatility -f lab5.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003ee8d070 -D .  
```

Surprisingly, this yields three files with the extensions `.dat`, `.ycab`, and `.img`. We initially focus on the `.dat` file.

Upon checking the file type, we discover that it is a portable executable (PE). We rename it to `NOTEPADA.exe`:

```bash
file NOTEPADA.exe  
```

To analyze its contents, we use IDA (Interactive Disassembler). IDA is a powerful reverse engineering tool used to disassemble executables and analyze their underlying assembly code. This allows us to inspect malware or suspicious binaries at a low level.

```bash
ida NOTEPADA.exe  
```

IDA opens a pop-up where we proceed to view the code of the executable. Within the code, we find the `Stage3` flag revealed letter by letter:

```txt
b10s_m3m_l4b5_0v3r  
```

---

## Retrieving the First Flag

Since we have exhausted all suspicious files, we try a hit-and-trial approach by capturing screenshots from the memory dump:

```bash
volatility -f lab5.raw --profile=Win7SP1x64 screenshot -D .  
```

This produces multiple files, which we open in GIMP:

```bash
gimp *  
```

Upon cycling through the images, we find one where the window title contains a base64 string (image placeholder).

We carefully copy the string and decode it to reveal the `Stage1` flag:

```txt
flag{!!w3LL_d0n3_St4g3_0f_L4B_D0n3_!!}  
```

---

## Extracting Stage2.png

Using the first flag as the password, we extract `Stage2.png` from the RAR file:

```bash
unrar e file.rar  
```

Opening the extracted image in GIMP reveals the `Stage2` flag, completing the challenge.
