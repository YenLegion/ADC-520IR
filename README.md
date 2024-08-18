# Alarm.com ADC-520IR aka Vivotek IP8136 
How to repurpose old Alarm.com camera without a subscription. 

I've had this ipcam for as long as I can remember, think I got it at a garage sale. Thought it was useless till i learned of [this exploit](https://www.exploit-db.com/exploits/29516) which allows access to RTSP streams without authentication (wired). That's great, I can watch the stream, but I want to change SETTINGS! 

A scan of this device reveals ports 21, 23, 80, 554, 8080 as open. We have telnet. 

I think it has been out for some time that Alarm.com default login credentials on at least older devices is 'root/adcvideo'. Firmware version I have is '0100p2'. 

Telnet login works using the above credentials. We have root access. 

How to enable the WebUI: 

In /etc/conf.d there are a bunch of XML files. 

Make a copy of config_network.xml

# cp config_network.xml config_network.xml.bak

Edit config_network.xml - [Bonus](http://www.linux-admins.net/2011/01/vi-cheat-sheet.html)

# vi config_network.xml

Towards the end of the file you will find these lines of text.

<http>
      <anonymousviewing>0</anonymousviewing>
      <webaccess>0</webaccess>
</http>

Change the 0's to 1's.

Restart the camera, go to the IP address the camera is using in your browser and behold the WebUI in all it's glory. 

Under the "Configuration" tab can be found all the adjustable parameters for the camera. No more messing with XML files! 

