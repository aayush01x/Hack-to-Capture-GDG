# MemLabs Lab-2 – Writeup  

We begin by downloading the memory dump provided in the lab description and renaming it as `lab2.raw` for easier reference.  

## Initializing the Memory Dump  

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:  

```bash
volatility -f lab2.raw imageinfo  
```  

The output provides various data points about the image, including seven suggested service profiles in this case. One of these profiles must be chosen for subsequent commands.  

We select the first profile (`Win7SP1x64`). If any issues arise during the process, we can switch to the other profiles later.  

## Using Basic Plugins  

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).  

```bash
volatility -f lab2.raw --profile=Win7SP1x64 pslist  
```  

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, among them, a few suspicious processes stand out. These are:  
- **keepass.exe** – suggests password access/creation (referenced in the lab description).  
- **notepad.exe** – referenced in the description (possibly to inspect files).  
- **chrome.exe**  
- **cmd.exe**  

## Digging into keepass.exe  

We attempt to find the arguments passed to the process (i.e., the file to be opened) using the `cmdline` plugin:  

```bash  
volatility -f lab2.raw --profile=Win7SP1x64 cmdline  
```  

In the output (see image placeholder 0), `keepass.exe` is passed a file named **Hidden.kdbx**. This is an encrypted file, as seen by the failed attempt at opening it in Notepad (indicated in the `cmdline` output).  

Now, we try to extract the file to our local machine using the `filescan` and `dumpfiles` commands:  

``` bash 
volatility -f lab2.raw --profile=Win7SP1x64 filescan | grep -i hidden.kdbx  
volatility -f lab2.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fb112a0 -D .  
```  

We rename the file to `Hidden.kdbx` and try to open it using the `keepass2` command:  

```bash  
keepass2 Hidden.kdbx  
```  

A KeePass application popup appears, prompting for a password (see image placeholder 1).  

## Searching for the Password  

Following hints from the description, we investigate the environment variables of the dump using the `envars` plugin:  

```bash  
volatility -f lab2.raw --profile=Win7SP1x64 envars  
```  

In the output, we find a variable named **NEW_TEMP** with the value:  

```txt
ZmxhZ3t32xjMGĐzX10wXyRUNGzXyFfT2ZfTDRCXzJ39
```  

This appears to be a Base64 string. We decode it using standard `echo` and `base64` commands:  

```  bash
echo ZmxhZ3t32xjMGĐzX10wXyRUNGzXyFfT2ZfTDRCXzJ39 | base64 -d  
```  

This reveals our first flag:  

```txt
flag{w31c0m3_To_ST4g3_1_0f_L4B_2}
```  

## Continuing the Password Search  

Next, we theorize that the password might have been copied and pasted by the user, so it could exist in the clipboard. We extract clipboard contents using the `clipboard` plugin:  

```  bash
volatility -f lab2.raw --profile=Win7SP1x64 clipboard  
```  

(See image placeholder 2). Unfortunately, nothing of value is found in the clipboard.  

We then search for files containing the word "password" in their name using `filescan` and `grep`:  

``` bash 
volatility -f lab2.raw --profile=Win7SP1x64 filescan | grep -i password  
```  

(See image placeholder 3). In the output, we find a file named **password.png**. We extract it using the `dumpfiles` command and rename it:  

```  bash
volatility -f lab2.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fce1c70 -D .  
mv file.None.0xfffffa8003d7b6d0.dat password.png  
```  

Opening the PNG in GIMP, we inspect the bottom-right corner to find the password (see image placeholder 4).  

Returning to `Hidden.kdbx`, we open it with `keepass2` and enter the obtained password. This unlocks the hidden directory, revealing different sections. In the Recycle Bin, we find an entry titled "sabka baap" with the username "flag." Copying the hidden password gives us the second flag:  

```txt
flag{w0w_th1s_1s_Th3_SeC0nD_ST4g3_!1}
```  

## Finding the 3rd Flag  

Now, we investigate `chrome.exe`. To extract its user history, we download a separate plugin package containing `chromehistory`:  

```  bash
volatility --plugins=../volatility_plugins -f lab2.raw --profile=Win7SP1x64 chromehistory  
```  

In the output, we find a suspicious Mega link:  

```  txt
https://mega.nz/#F!TrgSQOTS!H0ZrUzF0B-2KNM3y9E761g  
```  

We open the link and download a ZIP file named **important.zip**. To extract it, we use `7zz`:  

```  bash
7zz e important.zip  
```  

The extraction prompts for a password and displays a comment stating that the password is the SHA1 hash of the stage 3 flag from Lab 1. We convert the stage 3 flag from Lab 1 into its SHA1 hash:  

```  bash
echo -n "flag{example_stage3}" | sha1sum  
```  

Entering the hash as the password extracts a PNG file named **important.png**. Opening it in GIMP reveals the third flag, completing the challenge.  

``` txt
flag{f1n4l_st4g3_c0mpl3t3}
```  

(See image placeholder 5).

