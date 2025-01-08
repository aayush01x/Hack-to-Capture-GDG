After reading the sample lab0's writeup one thing which emphasized on is the description of the problem gives you hints and potential approaches , so following this I noticed some things like "black window pop up with some thing being executed" should be cmd according to me and the fact that "When the crash happened, she was trying to draw something." most probably should be MS - Paint.
```
 vol -f lab.raw windows.info      
```
The above displays the general info about the Windows OS that was in use and I found that it is a Win7SP1x64 system. 
```
vol -f lab.raw windows.pslist
```
The above lists the processes that were going on just before the crash and I found some processes that look of interest to me . First is obviously cmd.exe which was being executed , we also had ms-paint.exe running along with a WIN-Rar file which looks suspicious.

I wanted to check what commands were being executed on the cmd as they told us that suddenly black window appeared and everything crashed , but I'm facing issues in finding the commands which will give me the info. I know the commands for volatility 2 but I was not able to find its equivalent and hence was not able to proceed with the other parts
