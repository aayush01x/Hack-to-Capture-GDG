flag: flag{g1f_or_j1f}
```bash
$ xxd unopenable.gif
```
since the description of the challenge suggested some changes in the file bytes. Checked the magic bytes and they didn't match the one for gif. After unsuccesfully trying to change the first few bytes to the gif ones in hexed.it , tried prefixing with the missing bytes, which worked!