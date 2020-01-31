<!-- permalink: edb057798cffd1a7b02142ab4d6e12f5 DO NOT DELETE OR EDIT THIS LINE -->
# Windows Tips

### Active Directory Stuff

* Logon profile script location:
	* *C:\Windows\SYSVOL\sysvol\domain-name\scripts*
	* `\\servernameorip\netlogon`

### Better Event Viewer Queries

* [source here](http://serverfault.com/a/571977)
* [logon event id codes](https://www.sans.org/reading-room/whitepapers/forensics/windows-logon-forensics-34132) (ctrl-f for '4624')
* [turn logging on](http://www.howtogeek.com/124313/how-to-see-who-logged-into-a-computer-and-when/)

### Env Variables (even for non admin)
* `rundll32 sysdm.cpl,EditEnvironmentVariables`

### Hosts File Location

* `c:\Windows\System32\Drivers\etc\hosts`


### Hostname

Rename the computer name from comand line (if the computer is on a domain, it MUST have contact with the domain controller)

	wmic computersystem where name="%COMPUTERNAME%" call rename name="NEW-NAME" ## this didn't seem to work

or

	WMIC computersystem where caption='currentname' rename newname

### Log File Issue Fix
This is the issue where the drive just fills up with errant log files

This script works (in my quick utilities directory too)

	@echo off

	cd C:\Windows\logs\cbs
	del *
	cd c:\windows\temp\
	mkdir cabs
	move cab* cabs\
	rmdir /s cabs

[Reference](https://answers.microsoft.com/en-us/windows/forum/windows_7-files/cabxxxx-files-found-in-windowstemp-folder/2e86137e-7e6b-4cb7-9a3c-4ee73f665742) - 5kyFx's reply

### Printer Driver Install

When you are at the page to type in the TCP/IP address, be sure to change the dropdown from *Autodetect* to *TCP/IP Device* or whatever

### Remote Desktop Cache Location
* `%localappdata%\Microsoft\Terminal Server Client`
* if you are getting internal server errors when trying to connect to RDP, deleting this cache can fix it

### System Integrity
* check system files for corruption:
	* `sfc /scannow`
* check NTFS for integiry
	* `chkdsk /f`
		* runs on *C drive* upon reboot
	* `chkdsk /f D:`
		* runs on *D drive* - probably doesn't need to reboot


### Windows Domain Non Admin As Local Admin

Simply add the domain user to the administrators group in the local computer

(right click on computer, manage, local users and groups, administrators)
