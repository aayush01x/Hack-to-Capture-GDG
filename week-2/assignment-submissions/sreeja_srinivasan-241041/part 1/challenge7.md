we were given a zip file message.zip, which was unzipped using 
````
$unzip message.zip
````
on checking the type of file, we see that it is an ogg data audio file. This was converted to .wav by installing vorbis-tools package and using the oggdec command, which have us help.wav
````
$oggdec help.me
````

on visualizing this using a spectrogram in sonic visualizer, we get a qr code, which on scanning gives us the flag:
the_flag_is{A_sP3c7r0grAm?!}
