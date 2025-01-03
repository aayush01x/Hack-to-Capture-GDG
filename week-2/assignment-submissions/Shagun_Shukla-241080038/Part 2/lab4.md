# MemLabs Lab-4 – Writeup

We begin by downloading the memory dump provided in the lab description and renaming it as `lab4.raw` for easier reference.

---

## Initializing the Memory Dump

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:

```bash
volatility -f lab4.raw imageinfo  
```

The output provides various data points about the image, including seven suggested service profiles. One of these profiles must be chosen for subsequent commands.

We select the first profile (`Win7SP1x64`). If any issues arise during the process, we can switch to the other profiles later.

---

## Using Basic Plugins

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).

```bash
volatility -f lab4.raw --profile=Win7SP1x64 pslist  
```

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, one suspicious process stands out:

- `StiickyNot.exe`

The unusual spelling (`StiickyNot.exe` instead of `StickyNotes.exe`) raises suspicion, suggesting potential tampering or malicious intent.

---

## Digging into StiickyNot.exe

To investigate further, we attempt to retrieve the arguments passed to the `StiickyNot.exe` process. This can reveal file paths or commands that may provide more context about the process.

We use the `cmdline` plugin to inspect command-line arguments:

```bash
volatility -f lab4.raw --profile=Win7SP1x64 cmdline  
```

Surprisingly, this leads to a dead end as no arguments were passed to the `StiickyNot.exe` process.

To explore another avenue, we check the clipboard content, as suspicious data might have been copied there.

```bash
volatility -f lab4.raw --profile=Win7SP1x64 clipboard  
```

Unfortunately, the clipboard returns empty, indicating no actionable data.

---

## Trying the Screenshot Plugin

Since the usual approaches are ineffective, we pivot to a less conventional method – the `screenshot` plugin. This plugin captures the visual state of the system at the time of the memory dump. It won’t provide a direct screen capture but will reveal text fragments and outlines of open windows.

```bash
volatility -f lab4.raw --profile=Win7SP1x64 screenshot -D .  
```

The command dumps multiple files to the current directory.

**Note:** Many of these files will be blank or contain minimal information. We must manually inspect each to find useful data.

To open the dumped files, use:

```bash
gimp *  
```

Cycle through the files until relevant content appears.

Upon inspection, one of the images reveals a `dumpit.exe` window. The screen also displays the presence of a user account named `eminewwm`.

Although this detail seems minor, it could be useful for identifying relevant files later.

---

## Hit and Trial – Locating Suspicious Files

Since previous methods yield limited results, we perform a broad search for files under the `Users` directory that could hold valuable information. This includes files with extensions such as `.png`, `.jpg`, `.jpeg`, `.txt`, `.rar`, `.py`, or `.exe`.

```bash
volatility -f lab4.raw --profile=Win7SP1x64 filescan | grep -i '\\users\\' | grep -i png jpg jpeg txt rar py exe  
```

Three interesting files emerge:

1. `galf.jpeg` – Address: `0x000000003e8d19e0`
2. `Screenshot1.png` – Address: `0x000000003e912190`
3. `important.txt` – Address: `0x000000003fc398d0`

To dump these files, we use the `dumpfiles` plugin:

```bash
volatility -f lab4.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003e8d19e0,0x000000003e912190,0x000000003fc398d0 -D .  
```

After dumping, we notice that only two files (`galf.jpeg` and `Screenshot1.png`) are successfully retrieved. This indicates that the third file (`important.txt`) may have been deleted, aligning with the lab description suggesting that part of the challenge involves recovering deleted files.

---

## Retrieving the Deleted File

Deleting a file typically doesn't erase it but marks the storage location as available for overwriting. Until the space is overwritten, the data can often be recovered.

To retrieve the deleted `important.txt` file, we access the Master File Table (MFT). The MFT indexes file metadata, including file paths and starting locations.

We extract the MFT using the `mftparser` plugin and save the output to a file for easier analysis:

```bash
volatility -f lab4.raw --profile=Win7SP1x64 mftparser > mftdata  
```

Next, we search for `important.txt` in the dumped MFT data:

```bash
cat mftdata | grep -i important.txt -A 50  
```

**Note:** `-A 50` ensures we print the 50 lines following the occurrence of `important.txt`. This often reveals content or file paths.

---

## Extracting the Flag

The output includes a hex dump of `important.txt`, with segments of text embedded in the output.

Converting the hex data to readable ASCII reveals the flag, successfully completing the challenge.
