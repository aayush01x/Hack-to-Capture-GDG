First I put the cat's image on aperisolve and it gave me an image which said Spectrogram and Cat!=Rar! . When I used binwalk I saw there is a rar archive . So after extracting all the files I got an audio file and rar archive , I saw that the file signature of rar file had been changed and was made Cat! instead of Rar! . Here is where the earlier image comes into picture that I should have a look at the spectogram of the audio file and indeed it had a password which was used to extract the files from the rar archive. We get a finally.txt which contains a base64 encoded string which is the flag. 
```
unrar x flag.rar  
```
#### PASSWORD FROM SPECTOGRAM - sp3ctrum_1s_y0ur_fr13nd ####
#### FLAG AFTER DECODING  - f0r3n51cs_ma5t3r ####

