flag: flag{w3ll_3rd_stage_was_easy}

```bash
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw imageinfo
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 crashinfo
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 cmdline
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 cmdscan
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 filescan | grep Important
$ mkdir dump dump2 dump3
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fa3ebc0 --dump-dir=dump2
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fac3bc0 --dump-dir=dump
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fb48bc0 --dump-dir=dump3
$ cd dump && ls
$ file file.None.0xfffffa8001034450.dat
$ volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 hashdump
$ unrar e file.None.0xfffffa8001034450.dat
```
crashinfo: nothing interesting
cmdline: Important.rar was made
cmdscan: St4G3$1 strange
while unraring the hint was that the password is the NTLM hash.
unraring gave flag3.png which had the flag