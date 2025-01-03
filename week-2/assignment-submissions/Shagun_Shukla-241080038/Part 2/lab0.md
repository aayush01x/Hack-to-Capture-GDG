# MemLabs Lab-0 – Writeup  

We begin by downloading the memory dump provided in the lab description and renaming it as `lab0.raw` for easier reference.  

## Initializing the Memory Dump  

First, we extract information about the memory dump using the `imageinfo` plugin of Volatility:  

``` bash
volatility -f lab0.raw imageinfo  
```  

The output provides various data points about the image, including three suggested service profiles. One of these profiles must be chosen for subsequent commands.  

We select the first profile (`Win7SP1x86_23418`). If any issues arise during the process, we can switch to the other profiles later.  

## Using Basic Plugins  

Next, we list all processes that were running when the memory dump was captured. This can be done using the `pslist` plugin, which is specific to Windows memory dumps (for Linux and macOS, `psaux` or `pframe` is used).  

``` bash 
volatility -f lab0.raw --profile=Win7SP1x86_23418 pslist  
```  

The output shows a list of common Windows processes like `dumpit.exe` and `conhost.exe`. However, among them, a few suspicious processes stand out.  

One such process is `cmd.exe`, indicating that the command line was active when the memory dump occurred.  

## Digging into cmd.exe  

To investigate further, we retrieve the command history from the memory dump. This is done using the `cmdscan` plugin, which extracts the command history for applications like `cmd.exe` and `dumpit.exe`.  

```  bash
volatility -f lab0.raw --profile=Win7SP1x86_23418 cmdscan  
```  

Under the `cmd.exe` section, we find an interesting entry:  

``` bash 
Cmd #0 @ 0x2f43c0: C:\Python27\python.exe C:\users\hello\Desktop\demon.py.txt  
```  

This reveals that a Python script named `demon.py.txt` was executed.  

## Demystifying demon.py.txt  

To see if any input was provided to the script and to check the output, we use the `consoles` plugin. This plugin shows the inputs and corresponding outputs of commands executed in the command line.  

```  bash
volatility -f lab0.raw --profile=Win7SP1x86_23418 consoles  
```  

The output shows that no input was given to `demon.py.txt`, but the script produced the following output:  

```  txt
335d366f5d6031767631707f  
```  

At first glance, this appears to be a hexadecimal string, potentially representing a hash.  

To analyze the string, we use **CyberChef** to check if it corresponds to any known hash. Unfortunately, no matches are found.  

Next, we attempt to decode the string as hexadecimal. This results in the following output:  

```  txt
3]60]’1vv1p  
```  

While this is not readable, it may indicate encrypted text. We decide to continue exploring for more clues.  

## Digging Deeper  

Upon revisiting the lab description, we notice references to **environment variables**. This hints at the possibility of relevant information being stored in the environment variables of running processes.  

We use the `envars` plugin to list all environment variables.  

```  bash
volatility -f lab0.raw --profile=Win7SP1x86_23418 envars  
```  

Among the variables, we discover one named `thanos` (mentioned in the lab description), with the value:  

```  txt
xor and password  
```  

This suggests that the previously retrieved text may be XOR-encrypted.  

Using CyberChef’s **XOR Brute Force** tool, we decrypt the string by testing all possible key values. With a key of `02`, the output decodes to:  

```txt
I_4m_b3tt3r}  
```  

This clearly appears to be the second half of the flag.  

## The Quest for the First Part  

Since the second part of the `thanos` variable (`password`) helped decrypt the string, the first part (`xor`) may provide further clues.  

Next, we attempt to extract password hashes using the `hashdump` plugin. This plugin retrieves password hashes of users currently logged in.  

```  bash
volatility -f lab0.raw --profile=Win7SP1x86_23418 hashdump  
```  

In the results, we identify a non-default user named `hello`, which stands out.  

We try cracking the NTLM hash of this user (as LM hashes are often the same across all users) using **John the Ripper**. Unfortunately, no matching passwords are found.  

## A Dead End  

After spending considerable time attempting to crack the password using various tools and websites (like CrackStation), we consult the sample solution from MemLabs' GitHub repository.  

A pull request reveals that others faced the same issue – the relevant password cracking websites no longer store the data required to crack the NTLM hash of Lab-0. This makes it impossible to proceed further.  

Thus, Lab-0 concludes unsatisfactorily, with the second part of the flag and the NTLM hash discovered but without the complete flag.
