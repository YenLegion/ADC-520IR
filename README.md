# Alarm.com ADC-520IR aka Vivotek IP8136 
### How to repurpose old Alarm.com camera without a subscription. 


I've had this ipcam for as long as I can remember, think I got it at a garage sale. 

Thought it was useless till i learned of [this exploit](https://www.exploit-db.com/exploits/29516) which allows access to RTSP streams without authentication (wired). 

That's great, I can watch the stream, but I want to change SETTINGS! 

Firmware version I have is '0100p2'. 

## How to enable the WebUI: 

Start by resetting the camera. There is a reset button on the back, can't miss it. 

Plug ethernet cable into camera, let DHCP allocate an IP address to the camera. Find the address with Nmap or through your router. 

Initially telnet is not enabled. To enable telnet go to http://IP_ADDRESS/cgi-bin/admin/mod_inetd.cgi?telnet=on

Alarm.com default login credentials, at least on older devices, are 'root/adcvideo'. Enter those when the prompt appears.

Now a scan of the device reveals ports 21, 23, 80, 554, 8080 as open. We have telnet on port 23.

Telnet login works using the same credentials. We have root access. 

In /etc/conf.d there are a bunch of XML files. 

Make a copy of config_network.xml
```
# cp config_network.xml config_network.xml.bak
```
Edit config_network.xml - [Bonus](http://www.linux-admins.net/2011/01/vi-cheat-sheet.html)
```
# vi config_network.xml
```
Towards the end of the file you will find these lines of text.
```
<http>
      <anonymousviewing>0</anonymousviewing>
      <webaccess>0</webaccess>
</http>
```
Change the 0's to 1's.

Restart the camera, go to the IP address the camera is using in your browser and behold the WebUI in all its glory.
