# MemLabs Lab-1 – Writeup

We begin by downloading the memory dump provided in the lab description and renaming it as `lab1.raw` for easier reference.

## Initializing the Memory Dump

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:

```bash
volatility -f lab1.raw imageinfo  
```

The output provides various data points about the image, including seven suggested service profiles in this case. One of these profiles must be chosen for subsequent commands.

We select the first profile (`Win7SP1x64`). If any issues arise during the process, we can switch to the other profiles later.

## Using Basic Plugins

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).

```bash
volatility -f lab1.raw --profile=Win7SP1x64 pslist  
```

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, among them, a few suspicious processes stand out. These are:

- `winRAR.exe` (suggesting archiving or accessing an archive during the process)
- `mspaint.exe` (referenced in the lab description)
- `cmd.exe` (possibly linked to the system crash, as the description mentions a black window popping up)

## Digging into cmd.exe

To investigate further, we retrieve the command history from the memory dump. This is done using the `cmdscan` plugin, which extracts the command history for applications like `cmd.exe` and `dumpit.exe`.

```bash
volatility -f lab1.raw --profile=Win7SP1x64 cmdscan  
```

Under the `cmd.exe` section, we find an interesting entry:

```bash
Cmd #0 @ 0x1de3c0: St4G3$1    
```

This command is not a standard Windows command. This leads us to two possibilities: either there exists an `.exe` file with this name that was executed, or it is a custom command created by the user.

## Demystifying St4G\$1

To check if any input was provided to this command and to see the corresponding output, we use the `consoles` plugin. This plugin shows the inputs and outputs of commands executed in the command line.

```bash
volatility -f lab1.raw --profile=Win7SP1x64 consoles  
```

The output reveals no input was provided, but the command produced the following output:

```txt
ZmxhZ3t0aDFzXzFzX3RoM18xc3Rfc3Q0ZzMhIX0=  
```

This appears to be a base64-encoded string.

To decode it, we use the following command:

```bash
echo ZmxhZ3t0aDFzXzFzX3RoM18xc3Rfc3Q0ZzMhIX0= | base64 -d  
```

This gives us the first of the three flags required for the lab:

```txt
flag{this_1s_th3_1st_st4g3!!}  
```

## Digging Wider for Flag 2

Next, we shift focus to `mspaint.exe`. We attempt to dump the memory of the entire process, hoping that the image being created or edited provides a clue to the next flag.

We note the process ID of `mspaint.exe` (2424) and use the `memdump` plugin:

```bash
volatility -f lab1.raw --profile=Win7SP1x64 memdump -p 2424 -D .  
```

(`-D .` dumps the memory in the current directory)

Running `ls`, we find a file named `2424.dmp`. We change its extension to `.data` to open it in GIMP:

```bash
mv 2424.dmp 2424.data  
```

Now, we open the file in GIMP:

```bash
gimp 2424.data  
```

The image initially appears as gibberish. This is because the memory dump of `mspaint.exe` includes various application data, not just the image.

To retrieve the image correctly, we adjust the width and offset values. After research, the correct values were found to be:

- Offset = 6774541
- Width = 1230

We obtain the following image, which reveals the second flag:

*Image Placeholder 0*

## Quest for the 3rd Flag

Finally, we investigate the `winRAR.exe` process. We attempt to find the arguments passed to this process, such as the file being archived. This is done using the `cmdline` plugin:

```bash
volatility -f lab1.raw --profile=Win7SP1x64 cmdline  
```

For `winRAR.exe`, we find the following command:

```bash
WinRAR.exe pid: 1552  
Command line: "C:\Program Files\WinRAR\WinRAR.exe" "C:\Users\Alissa Simpson\Documents\Important.rar"  
```

Next, we extract this file from the memory dump using the `filescan` plugin, paired with `grep` to locate it:

```bash
volatility -f lab1.raw --profile=Win7SP1x64 filescan | grep -i important.rar  
```

The file and its location are revealed:

*Image Placeholder 1*

Now, we dump the file using the `dumpfiles` plugin:

```bash
volatility -f lab1.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fa3ebc0  
```

Running `ls`, we see the file. We rename it to `.rar` and extract its contents:

```bash
mv 0x000000003fa3ebc0 Important.rar  
unrar e Important.rar  
```

The extracted archive contains `flag3.png`, but it is password-protected.

*Image Placeholder 2*

Following the hint, we dump user password hashes using `hashdump`:

```bash
volatility -f lab1.raw --profile=Win7SP1x64 hashdump  
```

We retrieve Alissa’s NTLM hash, convert it to uppercase using CyberChef’s “To Uppercase” function, and use it as the password to unlock the archive.

Opening `flag3.png` in GIMP reveals the third and final flag:

*Image Placeholder 3*

Challenge complete.