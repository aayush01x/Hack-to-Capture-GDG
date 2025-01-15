### MemLabs Challenges

```bash
# MemLabs Lab 0
volatility -f Challenge.raw imageinfo
volatility -f Challenge.raw --profile=Win7SP1x86 pslist
volatility -f Challenge.raw --profile=Win7SP1x86 cmdscan
# Output: C:\Python27\python.exe C:\Users\hello\Desktop\demon.py.txt
volatility -f Challenge.raw --profile=Win7SP1x86 consoles
volatility -f Challenge.raw --profile=Win7SP1x86 envars
volatility -f Challenge.raw --profile=Win7SP1x86 hashdump
# Flag: flag{you_are_good_but1_4m_b3tt3r}

# MemLabs Lab 1
volatility -f MemoryDump_Lab1.raw imageinfo
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 procdump -p <process-id> --dump-dir <directory>
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 cmdscan
volatility -f MemoryDump_Lab1.raw --profile=Win7SP1x64 console
# Flag: flag{th1s_1s_th3_1st_st4g3!!}

# MemLabs Lab 2
volatility -f MemoryDump_Lab2.raw imageinfo
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 filescan | grep kdbx
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003fb112a0 --dump-dir <directory>
volatility -f MemoryDump_Lab2.raw --profile=Win7SP1x64 envars
# Flag: flag{w3lc0m3_T0_$T4g3_!_Of_L4B_2}

# MemLabs Lab 3
volatility -f MemoryDump_Lab3.raw imageinfo
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 pstree
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 cmdline
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 filescan > mem3_filescan.txt
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000003de1b5f0 -D
volatility -f MemoryDump_Lab3.raw --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000003e727e50 -D
# Flag: inctf{0n3_h4lf_1s_n0t_3n0ugh}

# MemLabs Lab 4
volatility -f MemoryDump_Lab4.raw imageinfo
volatility -f MemoryDump_Lab4.raw --profile=Win7SP1x64 pslist
vol.py -f MemoryDump_Lab4.raw --profile=Win7SP1x64 mftparser > mem4_mft.txt
volatility -f MemoryDump_Lab4.raw --profile=Win7SP1x64 mftparser > mft.txt
# Flag: inctf{1_is_n0t_EQu4l_7o_2_bUt_th1s_d0s3nt_m4ke_s3ns3}

# MemLabs Lab 5
volatility -f MemoryDump_Lab5.raw imageinfo
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 cmdline
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 netscan
volatility -f MemoryDump_Lab5.raw --profile=Win7SP1x64 iehistory
# Flag: flag{!!_w3LL_d0n3_St4g3–1_0f_L4B_5_D0n3_!!}

# MemLabs Lab 6
volatility -f MemoryDump_Lab6.raw imageinfo
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 pslist
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 cmdline
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 filescan > mem6_filescan.txt
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000005fcfc4b0 -D
volatility -f MemoryDump_Lab6.raw --profile=Win7SP1x64 consoles
# Flag: inctf{thi5cH4LL3Ng3_!s_g0nn4_b3_?_aN_Am4zINg_!_i_gU3Ss???}
