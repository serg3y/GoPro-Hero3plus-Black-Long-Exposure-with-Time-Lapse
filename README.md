# GoPro-Hero3plus-Long-Exposure-with-Time-Lapse

I see many versions of gopro autoexac scripts and none work on my Hero3+Black. I made some changes and the attached code works for me. The code belongs in an "autoexac.ash" file that must be placed in the root directory of the SD card. The code starts running when camera is turned on and not charging. Camera will accept user commands while the script is running a "sleep" command. There are many restrictions on the file format some of which are listed here.

-------------------------------
> 1. sleep 3                               #wait for boot menu screen to clear (1-3 sec)'
> 2. t app appmode photo                   #switch to photo mode
> 3. sleep 1                               #wait for photo mode change to take place (works 95% of the time without this)
> 4. t ia2 -ae still_exp ISO ExposureCode  #set ISO and ExposureCode = -ln(ExposureTime/8)*182
> 5. t app button shutter PR               #start exposure
> 6. sleep 10                              #wait for exposure to end (up to 8 sec), and for image to be processed (1-2 sec)
> 7. reboot yes                            #restart GoPro and run the script again

--------------------------------
                                       
Time(sec) |TimeCode
----------|---------
0.033     |     999
0.05      |     924
0.1       |     798
0.2       |     671
0.5       |     505
1         |     378
2         |     252
5         |      86
8         |       0
