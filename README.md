# GoPro Hero3+ Black: Long Exposure with Time Lapse

There are many versions of gopro scripts for long exposure and time lapse but each seems to have something wrong with it for useing with Hero3+Black. So here is my version. The code belongs in an "autoexac.ash" file, which must be placed in the root directory of the SD card. The code starts running when camera is turned on *if it is and not charging*. Camera will accept user commands while the script is running "sleep" commands. There are many restrictions on the file format some of which are listed here. Time lapse is achieved by rebooting at the end of the script. Time lapse can also be achieved by repeating commands, hoever the limit on maximum file length is rather short, and if exceeded the script will not start. (I don't know if the limit is charecter or line or command based).

> 1. sleep 3                               #wait for boot menu screen to clear (1-3 sec)
> 2. t app appmode photo                   #switch to photo mode
> 3. sleep 1                               #wait for photo mode change to take place (works 95% of the time without this)
> 4. t ia2 -ae still_exp ISO ExposureCode  #set ISO and Exposure
> 5. t app button shutter PR               #start exposure
> 6. sleep 10                              #wait for exposure (up to 8 sec), and image to be processed (1-2 sec)
> 7. reboot yes                            #restart GoPro and run the script again

Tested on HERO3+ Black Edition, firmware version:"HD3.11.03.00" and "HD3.11.02.00"

ExposureCode = -ln(ExposureTime/8)*182

ExposureTime = 8*exp(-ExposureCode/182)

ExposureCode must be rounded to the nearest integer and in the range [0 1000]

ExposureTime (sec)|ExposureCode
------------------|---------
0.033             |     999
0.05              |     924
0.1               |     798
0.2               |     671
0.5               |     505
1                 |     378
2                 |     252
5                 |      86
8                 |       0

Line Feeds:
- You must use Linux style line feed to end each line, this is ascii code 10, often referred to as "/n" in computer codes
- Windows style line breaks, /r/n, will crash the scrip! To correct use notepad++, go to edit>EOL conversion>Unix.
- The last line in the script must end in a line feed, else it will not execute!
- You can have blank lines to separate code segments

General:
- To convert a desired exposure time into exposure code: code = round(-ln(time_in_sec/8)*182) in the range [1 to 1000]
- Turning on the camera while it is charging will not trigger the execution of autoexec.ash! However autoexec.ash will continue to run if camera is connected to power after it is turned on, but a reboot will stop execution.
- If the script does not have long sleep periods of 3+ seconds the user will not be able to shut down the camera gracefully.
- The camera does NOT wait for photo to be captured, so captures should be followed by a "sleep" that is longer than the exposure time (8 sec max) PLUS time needed to process the photo (1-2 sec).
- Having short or missing sleep periods will result in unreliable execution of the subsequent command. eg 1-3 sec sleep at the star, and 1 second sleep after changing camera mode.
- Camera light flashes at the end of the exposure, not at the start.

Commenting:
- Extra spaces after a command can be added and will be ignored.
- Comments using "#" either on a blank line or after a command can be added.
- COMMENT YOUR CODE!!!

Hardware:
- Camera may refuse to turn on because an expansion battery was connected to the camera while the camera was turned *off*. Remove expansion battery and MAIN BATTERY, wait 5-10 seconds, connect main battery, turn on GoPro and connect expansion battery *while camera is turned on*. Camera should now turn off and on properly, while expansion battery remains connected.
