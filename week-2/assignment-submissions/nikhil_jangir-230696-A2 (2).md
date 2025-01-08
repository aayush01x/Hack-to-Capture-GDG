# Task 1
 ## challenge 1
  - use anything from exiftool , strings , xxd etc. to get the flag :
     ```
     exiftool math.jpg
  The flag is : CTFlearn{I_Like_Math_2_5}
 ## challenge 2
  - Chnage the header of the file
     ```
    xxd unopenable.gif | less
    hexedit unopenable.gif
    xdg-open unopenable.gif    ## used to open file or an URL
  The flag is : flag{g1f_or_j1f}
 ## challenge 3 
  - Get a directory hidden inside the file then finding a hidden text in an image
     ```
     file Santa.rar
     binwalk -e Santa.rar
     file *
     eog *
  - "java -jar stegsolve.jar" command can be used to see the blur image
  Hidden text = "Winter is Coming"
 ## challenge 4 
  -  
 ## challenge 5 
  - use stegsolve to check that the there is hidden text bbehind that cat image "Spectogram  , cat! = rar! " . Then use binwalk to find any hidden directory . 
    ```
     java -jar stegsolve.jar     
     binwalk -M --dd=.*megatron.png  
     cd _megatron.png.extracted
     sonic-visualiser purrr_2.mp3      ## we got a password for a file = "sp3ctrum_1s_y0ur_fr13nd"
     hexedit y0u_4r3_cl0s3.rar     ## chane the header of this file to rar then unrar it using the password found . 
     unrar e y0u_4r3_cl0s3.rar    ## we got file that contains the flag 
     cat f1n4lly.txt   ## This contains a base64 encoded flag , use cipher decoder to decode it .
  The flag is : f0r3n51cs_ma5t3r  
 ## challenge 6
  - 
 ## challenge 7 
  - flag from the qrcode found the spectogram of help.ogg . Using GIMP to enhance the qrcode that is readble to the "zbarimg"  
     ```
     file message.zip 
     7z x message.zip  ## unzip everything 
     cd seeingisbelieving  
     cp help.me help.ogg
     sonic-visualiser help.ogg   ## we got an qrcode from the spectogram of this "mplayer" 
     zbarimg flag.png 
  The flag is : the_flag_is{A_sP3c7r0grAm?!}
 ## challenge 8 
  - 
 ## challenge 9 
  -  
 ## challenge 10 
  - flag finding using Morse code decoder . Identy the morse code pattern in the spectogram and decode it 
     ```
     java -jar stegsolve.jar
  The flag is "MORSE CODE FTW"    
 ## challenge 11
  - 
    ```
    file secret.file
    7z2john secret_file > secret_file.hash
    john --wordlist=rockyou.txt secret_file.hash
    cat flag(81).txt
    touch image.base64
    nano image.base64
    base64 -d image.base64 > image.bmp
    eog image.bmp
  The flag is : fastctf{the hashcat goes meow}
  ---
# Task 2
  ---
# Task 3 (OSINT)

 ## OSINT 1
  - search ( kiffa , arab ) at google , copy the cordinates and use google earth pro to find the exact coordinates of place. The coordinates of where photo was taken are 
    nearby  “16.609504, -11.397878”.
 ## OSINT 2
  - Flinders Street Railway Station 
  - Name of the building: Arts Centre Melbourne(162m)
  - Search Flinders street written at the board . Then copy the cordinates and use google earth pro to find the height and name of the tallest statue which lookes like an 
    mobile tower not the building that is at the top right corner of the image .
 ## OSINT 3
  - The place is the Turkish Presidential Complex
  - Its coordinates is nearby 39.9308°N 32.7989°E
  - search on Google Lens , where turkish president receives visitors , then use google earth pro to find the exact coordinate.
 ## OSINT 4
  - Oan Resort
  - 7°21'45.65"N , 151°45'22.61"E
  - Northwest
  - A quick reverse image search gives a website with same thumbnail then use google earth to find the coordinates of the island and the cardinal directions .
 ## OSINT 5
  - Polar bear Plunge , San Diego Zoo
  - 32.734467° N, 117.154591° W
  - 17.0°C ( google to find the data for temp.)
  - reverse image search quickly gives the details about the zoo , then visit the website to see the polar bear live camera from which photo was captured and get the exact 
    locations using google earth pro .
 ## OSINT 6
  - The above image is a fake news
  - Doing reverse image search we get the same image but the date and the news are different . This image is of bombing in iraq not somthing in khyber city .
 ## OSINT 7 
  - Centro Vasco da Gama (use google lens to find out the eaxct location)
  - The largest letters on the poster say Tutankamon, so I put the term in a Google search. Searching in English didn't give the desired results, so I switched 
    my Google to the native language of Portuguese and found this poster on google which looks like a movie poster , it's release date and link below the poster .
  -  somewhere beetween (march - april) 2019
  -  www.tutankamon.pt
 ## OSINT 8
  - Shen Yun , ancient Chinese culture and dance
  - Jan 13–14, 2024 .
  - Norfolk's Chrysler Hall
  - reverse image search will give me the details about the place where the event was happening , then use google translater to everything else .
 ## OSINT 9
  - Between 4:56 PM and 5:31 PM ( Searching about when suset happens in kavaja ) 
  - 41°19'36.67"N ,  19°48'25.89"E 
  - using google lens we get the same place and it's location . Then use google earth pro to know about the exact coordiantes where the video was recorded.
 ## OSINT 10 
  - VOODOO FESTIVAL
  - The left one and the below right are caputerd by same photographer (using reverse image search we found that they are uploaded on same website on jan 9, 2012 by same 
    photograper (Ouidah benin)
  - Cotonou (searching all the photos of about the same timeline we found that photographer uploaded an photo on 6 jan , 2012 in the Cotomou city which is very near to 
    Ouidah benin






