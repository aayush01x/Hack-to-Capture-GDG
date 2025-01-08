flag: CTFlearn{Santa_1s_COming}

```bash
$ zsteg 3.png
```

this showed that there was some extradata at end of the png so ran

```bash
$ zsteg -E "extradata:0" 3.png > pic.png 
```

Then used stegsolve( after reading the guides at aperisolve) to get the image with the flag by xorring(had to take mirror image of the image obtained to get the flag) 1.png and pic.png