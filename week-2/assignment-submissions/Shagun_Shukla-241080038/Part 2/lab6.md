# MemLabs Lab-6 – Writeup

We begin by downloading the memory dump provided in the lab description and renaming it as `lab6.raw` for easier reference.

---

## Initializing the Memory Dump

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:

```bash
volatility -f lab6.raw imageinfo  
```

The output provides various data points about the image, including seven suggested service profiles. One of these profiles must be chosen for subsequent commands.

We select the first profile (`Win7SP1x64`). If any issues arise during the process, we can switch to the other profiles later.

---

## Using Basic Plugins

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).

``` bash
volatility -f lab6.raw --profile=Win7SP1x64 pslist  
```

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, a few suspicious processes stand out:

- `chrome.exe`
- `firefox.exe`
- `winRAR.exe`
- `cmd.exe`

---

## Digging into Processes

To investigate further, we attempt to retrieve the arguments passed to these processes. This can reveal file paths or commands that may provide more context about the process.

```bash
volatility -f lab6.raw --profile=Win7SP1x64 cmdline  
```

```bash
volatility -f lab6.raw --profile=Win7SP1x64 getsids -p <pid>  
```

Upon examination, we find that the file `flag.rar` in the `pr0t3ct3d` directory is associated with the `winRAR.exe` process. This is clearly important to us.

Additionally, several arguments are passed to Chrome and Firefox, but none appear immediately suspicious.

---

## Extracting the RAR File

As in previous labs, we extract the RAR file by using the following commands:

```bash
volatility -f lab6.raw --profile=Win7SP1x64 filescan | grep -i flag.rar
```

```bash
volatility -f lab6.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000005fcfc4b0 -D .
```

We rename the file:

```bash
mv file.None.0xfffffa8003d7b6d0.dat flag.rar
```

When attempting to extract `flag.rar`, it prompts for a password to access `flag2.png`. However, since we do not yet have the first flag, we cannot proceed with the extraction.

---

## Analyzing Browser History

To gather more leads, we analyze the Chrome history by using the `chromehistory` plugin (downloaded separately for Volatility):

```bash
volatility --plugins=../volatility_plugins/ -f lab6.raw --profile=Win7SP1x64 chromehistory
```

In the output, we scan for suspicious links and find a pastebin link: `https://pastebin.com/RSGSi1hk`.

The link references “david,” which is in the lab description, indicating that we are on the correct track. The link also leads to a Google Document. After scanning the document, we find a Mega link. However, the Mega link is encrypted and requires a decryption key that we do not possess.

---

## Retrieving the Key

Since no further leads are evident, we try capturing screenshots from the memory dump:

```bash
volatility -f lab6.raw --profile=Win7SP1x64 screenshot -D .  
```

The output produces multiple files, which we open in GIMP:

```bash
gimp *  
```

Upon reviewing the screenshots, we find one where the window title contains the text `Mega drive key` followed by an email address.

To retrieve this information programmatically, we search the memory dump for the phrase “mega drive key”:

```bash
strings lab6.raw | grep -i "mega drive key"  
```

In the output, we locate a decryption key preceded by the text “THE KEY IS”. Using this key, we access the Mega drive and download `flag_.png`.

When attempting to open the file in GIMP, it throws an error indicating a missing `IHDR` chunk, suggesting that the file's magic bytes have been tampered with.

---

## Repairing the PNG

To fix the file, we open it in `hexedit` and compare its hex dump to a standard PNG file. We manually adjust the `IHDR` portion:

```bash
hexedit flag_.png
```

Once corrected, the image opens successfully, revealing the first part of the flag:

```txt
inctf{thi5_cH4LL3Ng3_!s_g0nn4_b3_
```

---

## Finding the Second Half of the Flag

We attempt to extract `flag.rar` using the first half of the flag as the password, but it fails. This indicates that another password must be found.

We examine environment variables for potential passwords:

```bash
volatility -f lab6.raw --profile=Win7SP1x64 envars  
```

In the output, we find a variable named `RAR_PASSWORD`. Using its value, we successfully extract `flag2.png`:

```bash
unrar e flag.rar
```

Opening `flag2.png` in GIMP reveals the second part of the flag, completing the challenge:

```txt
aN_Am4zINg_!_i_gU3Ss???_}
```

---

### Final Flag:

```txt
inctf{thi5_cH4LL3Ng3_!s_g0nn4_b3_aN_Am4zINg_!_i_gU3Ss???_}
```


