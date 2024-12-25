### CHALLENGE 3 - SANTA'S SECRET ###
When we look at the first image it looks like two images being merged together. So when i ran binwalk on both images i found that an images is hidden in the second image which i extracted. On seeing the image it was a GOT night king image which seems to be present in the first images as well . So it was obvious that i had to take the difference of both the images to find the overlapped image. I used a online website https://www.img2go.com/compare-image
which gave me a mirror image of a flag.
```
binwalk -e 3.png
```
#### FLAG - CTFlearn{Santa_1s_C0ming} ####
