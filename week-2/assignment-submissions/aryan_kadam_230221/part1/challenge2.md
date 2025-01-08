### CHALLENGE 2 - CORRUPTION ? ###
As the name was unopenable.gif it made sense for me to check the hexdump file signature , opening which i found that it a part of the gif signature was missing (47 49 46 38), so i added it to the signature using the following command 
```
printf "\x47\x49\x46\x38" | cat - unopenable.gif > unopenable-fix.gif
```
When we open the fixed file we get a moving gif which contains a base 64 string , which i found by taking a screenshot of the moving frames and writing in down. Decoding it we get
#### FLAG - flag{g1f_or_j1f} ####
  
