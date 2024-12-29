# Challenge-1 : Equations
First check the file type using file command. The comment contains some useful info but it isn’t fully visible. So, use the strings command to get the printable characters in the header section of the file. Then, the 2 equations can be solved manually for getting the values of x and y.

```bash
$ file math.jpg
```

```bash
math.jpg: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, comment: "The flag for this challenge is of the form:", baseline, precision 8, 640x316, components 3
```

```bash
$ exiftool math.jpg
```

```bash
ExifTool Version Number         : 13.00
File Name                       : math.jpg
Directory                       : .
File Size                       : 191 kB
File Modification Date/Time     : 2024:12:25 13:55:09+05:30
File Access Date/Time           : 2024:12:25 13:56:22+05:30
File Inode Change Date/Time     : 2024:12:25 13:56:22+05:30
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : The flag for this challenge is of the form:..CTFlearn{I_Like_Math_x_y}..where x and y are the solution to these equations:..3x + 5y = 31..7x + 9y = 59...
Image Width                     : 640
Image Height                    : 316
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8                                                                                                                                                        
Color Components                : 3                                                                                                                                                        
Y Cb Cr Sub Sampling            : YCbCr4:4:4 (1 1)                                                                                                                                         
Image Size                      : 640x316                                                                                                                                                  
Megapixels                      : 0.202
```

```bash
$ strings math.jpg | head
```

```bash
JFIF
The flag for this challenge is of the form:
CTFlearn{I_Like_Math_x_y}
where x and y are the solution to these equations:
3x + 5y = 31
7x + 9y = 59
A#BQR
ab$3qr
5Ecs
1AQRb#aqr
```

```bash
CTFlearn{I_Like_Math_2_5}
```
