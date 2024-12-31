Extract Santa.rar to get 1.png and 3.png. Use binwalk on 3.png to see that it is hiding some PNG images.


```
binwalk 3.png
```


Use binwalk again to extract those PNGs.


```
binwalk --dd=".*" 3.png
```


You will get an image CCB6 which is similar to 1.png. Use stegsolve to combine the images to get an image. Mirror it to get the flag.

Flag - CTFlearn{Santa_1s_C0ming}