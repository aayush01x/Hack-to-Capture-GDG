flag: 0xL4ugh{W4RM_UP_STE94N0_G0OD_J0B}

Tried exiftool and binwalk on the jpg but didn't get anything useful. Nothing special through aperisolve.
Ultimately stegseek did the job

```bash
stegseek -sf image.jpg
file image.jpg.out
cat image.jpg.out
```