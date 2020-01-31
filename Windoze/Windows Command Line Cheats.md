# Command Line Cheats in Windows

### AD Remote Rename Computer

* These commands haven't been verified and might need to be run from the domain controller as it didnt work on my workstation

* `netdom renamecomputer currentcompname /newname:newcompname /userd:domain\admin /passwordd:* /usero:domain\admin /passwordo:* /reboot:10 /force`
* `netdom renamecomputer member /newname:member1.contoso.com /userd:administrator`


### Group Policy

* force update group policy
	* `gpupdate /force`

* Troubleshoot group policy for user *rsanchez*
	* `gpresult /u rsanchez /h file\path.html`
	* `rsop.msc` - in run window

### Networking

* List open ports
	* `netstat -aon | find /i "listening" | more`


### Passwords

* activate local admin
	* `net user administrator /active:yes`

* change user password for user *dvader* to *lightsaber123*
	* `net user dvader lightsaber123`
	* Be careful with special characters in the command line!


### Permissions
* deny *.git* folder to user noGitForYou
	* `icacls .git /deny "hostname\noGitForYou":(CI)(OI)(F,M,RX,R,W)`
	* [reference](https://technet.microsoft.com/en-us/library/cc753525%28v=ws.11%29.aspx)

* View all shares provided by computer:
	* `net share`

* View permissions of a share:
	* `net share <sharename>`

* View members of the current domain's group:
	* `net group <groupname> /domain`


### Print Text From File

	type file.txt

### Remote Reboot

1. Make sure you have the correct credentials for the remote system:
	* `net use \\computerNameOrIP /user:domain\username`
	* it will ask for password if your current credentials aren't valid
1. Run reboot command:
	* `shutdown /r /m \\computerNameOrIP /f /t 60`
		* `/r` = reboot (`/s` for shutdown)
		* `/m` = remote computer
		* `/f` = forced (doesn't ask users for permission or confirmation to log them out)
		* `/t` = number of seconds to delay before running operation
