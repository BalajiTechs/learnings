Ecllipse plugins for smart developement
http://www.modelgoon.org/update ( used for model view and flow detection)

hosts file in windows location C:\Windows\System32\Drivers\etc\hosts
To add startup bat script in windows, press WIN+r, and type shell:startup and press enter. copy the link of script in startup folder

==============================================================================================
Excel Tricks
1. CTRL+L ==> create table from sheet data
2. Convert all text to Lower
=LOWER(C8&".cloud.domain.in")

==============================================================================================
Eclipse problem
	1. Problem. Cannot install debug point as No line info found: 
Solution Please check if the deployed war is debug enabled or not. 
==============================================================================================

Reinstalling broken printer driver
remove the printer from device and printers(only printers not working). 
restart print spoolers  services(open services.msc-> printer spooler)
delete entries of printer from "print management->all_printers" and "print management->all_drivers"
Install new printer drivers

Restrict CPU usage of a process in linux
https://www.ostechnix.com/how-to-limit-cpu-usage-of-a-process-in-linux/

https://access.redhat.com/documentation/en-US/Red_Hat_Directory_Server/8.2/html/Administration_Guide/Managing_SSL.html

https://stackoverflow.com/questions/283608/using-regex-to-prefix-and-append-in-notepad
Addon-> Stop at first occurent of "S"  
	Ticket=([A-Za-z0-9].*?)\ S	


==============================================================================
WinDGB
https://debugbeyond.blogspot.com/2011/08/windbg-set-break-on-dll-load.html

To stop when a perticular dll is loaded
sxe ld:suspect.dll
g	

--------------------------------------------------------------------------------------------------
Find and replace duplicate lines from notepad++(npp)	
^(.*?)$\s+?^(?=.*^\1$)	

Find last occureance of a char in a line notepadd++(npp)
^.+/\K.+$   // search for last occurance of "/"