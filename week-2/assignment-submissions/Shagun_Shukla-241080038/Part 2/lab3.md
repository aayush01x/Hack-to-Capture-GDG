# MemLabs Lab-3 – Writeup

We begin by downloading the memory dump provided in the lab description and renaming it as `lab3.raw` for easier reference.

## Initializing the Memory Dump

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:

```bash
volatility -f lab3.raw imageinfo  
```

The output provides various data points about the image, including seven suggested service profiles in this case. One of these profiles must be chosen for subsequent commands.

We select the first profile (`Win7SP1x64`). If any issues arise during the process, we can switch to the other profiles later.

## Using Basic Plugins

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).

```bash
volatility -f lab3.raw --profile=Win7SP1x64 pslist  
```

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, among them, a few suspicious processes stand out. These are:

- `notepad.exe` (has 2 separate processes)

## Digging into notepad.exe

We attempt to find the arguments passed to both `notepad` processes, such as the names of the files opened with notepad. This is done using the `cmdline` plugin:

```bash
volatility -f lab3.raw --profile=Win7SP1x64 cmdline  
```

We see two sections for `notepad.exe`, where we see that `evilscript.py` and `vip.txt` are the two files opened in notepad.

Now by using the following combination of `filescan` and `grep` commands, we simultaneously find the file location of the two files in the hex dump:

```bash
volatility -f lab3.raw --profile=Win7SP1x64 filescan | grep -i "evilscript.py\|vip.txt"
```

This returns the values as:
- `0x000000003deb5f0` for `evilscript.py` 
- `0x000000003e727e50` for `vip.txt`

(We also find a location for `evilscript.py.lnk`, which seems to be a shortcut to the `evilscript.py` file.)

Now we dump the two files into our local machine using the familiar `dumpfiles` command:

```bash
volatility -f lab3.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003deb5f0 -Q 0x000000003e727e50
```

We use `ls` and `file` to identify which dumped file is what and rename them to their original names accordingly.

Now we print the data in the extracted `vip.txt` file using `cat`. This data seems to be in base64 encoding, so we decode it using standard commands:

```bash
cat vip.txt | base64 -d
```

However, the output we obtain is: 
```txt
jm'wex3m0\k7oe'
```
This is clearly not human-readable, leading to two possibilities:
- The data is encrypted.
- The data is not in standard base64 encoding.

## Reverse Engineering

Now we turn our attention to `evilscript.py`. Printing it using the console, we see that the script reads data from `vip.txt`, XORs the data with 3, then encodes it in base64, and rewrites it to `vip.txt`.

### Reasoning:
1. The script performs the following steps on the data:
   - XORs the data with the key `3`.
   - Encodes the XORed data in base64.
   - Writes the encoded data back to `vip.txt`.

2. To reverse the process:
   - We first decode the data from base64.
   - To undo the XOR operation, we XOR the decoded data again with `3` (since XORing twice with the same key reverts the original value).

Thus, to recover the original text, we follow the steps in reverse.

### Reverse Engineering Script:

```python
import base64

def xor(s):
    return ''.join(chr(ord(i)^3) for i in s)

def decoder(x):
    return base64.b64decode(x).decode()

if __name__ == "__main__":
    with open("vip.txt", "r") as f:
        arr = f.read()
    arr = xor(decoder(arr))
    print(arr)
```

Running this script prints out the first half of the flag:
```txt
inctf{0ne_h4lf
```
We keep this note as the lab description mentions that the first half of the flag is needed to get the second flag.

## Trying to use Steghide

As the challenge description hints at using `steghide`, we search for files that `steghide` can work with (i.e., `.jpg`, `.jpeg`, `.bmp`). We do this using `filescan` with `grep`:

```bash
volatility -f lab3.raw --profile=Win7SP1x64 filescan | grep -i "jpeg\|jpg\|bmp"
```

Upon searching through the list of files, we find an uncommon file named `suspicion1.jpeg` at address `0x000000004f34148`. We dump it using `dumpfiles` and rename it to `sus.jpg`:

```bash
volatility -f lab3.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000004f34148 -D ./
mv file.XXXXXX sus.jpg
```

Now we use `steghide` on the image: (I couldnt use it as i couldnt install it propery on my macbook so i refered to a writeup for the solution of this part)

```bash
steghide extract -sf sus.jpg
```

When prompted for a password, we input the first half of the flag (`inctf{0ne_h4lf`). This successfully extracts hidden data from `sus.jpg` and writes it to `secret.txt`.

Printing the contents of `secret.txt` reveals the second half of the flag:
```txt
_1s_n0t_3n0ugh}
```

Combining the two parts gives the final flag:
```txt
inctf{0ne_h4lf_1s_n0t_3n0ugh}
```
This completes the challenge.
