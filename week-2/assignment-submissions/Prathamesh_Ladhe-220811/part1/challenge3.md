## Challenge 3
### Writing only the succesful path
- Binwalk both the images 
-  First image had nothing
-  Second image 3.png had an image resembling the 1.png
- Extracted 3.png and got the CCB6 file
- 1.png and CCB6 appeared to be similar with some extra elements 
- A spherical object in the right bottom corner suggested to ->Used GIMP to import both the files, Opened as layer, set on on Difference mode , got the mirrored image with the flag , Rotated the image horizontally
Got the flag
```
CTFlearn{Santa_1s_C0ming}
```
