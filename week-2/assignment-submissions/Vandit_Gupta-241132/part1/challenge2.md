## Challenge 2

Here we were given a file which appeared to be a Gif but was currupt. Opening the file in Hexdump revealed that the file was missing the GIF8 characters at the begining, which I added using Kate Text Editor.
After the File was corrected, the Gif Gave a Base64 encoded message "ZmxhZ3tnMWZfb3JfajFmfQ==", which gave the flag: flag{g1f_or_j1f}


Note: The file given in the repo itself did not work after adding the signature, I used this file instead: https://mega.nz/#!aKwGFARR!rS60DdUh8-jHMac572TSsdsANClqEsl9PD2sGl-SyDk