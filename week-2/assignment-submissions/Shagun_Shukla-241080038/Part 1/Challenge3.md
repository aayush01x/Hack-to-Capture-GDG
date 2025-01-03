# Writeup

Used binwalk on 3.png which gave a hidden png file inside it.
```bash
$ binwalk -e 3.png
```

The extracted image seeemed like a clearer version of 1.png.

Used diff to check the diff between 1.png and the extracted file.
```bash
$ diff 1.png 2.png diff.png
```
diff.png saved the difference betweeen 1st file and second file which came out with the hidden flag.


Rotated it and found the flag as **CTFlearn{Santa_1s_COming}**
