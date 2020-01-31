# Rebuild User Profile

Be aware that there may be 3rd party apps that need to be installed into the user profile. (Gotomeeting, etc)

1. Reboot the computer
1. Log in as an admin
1. Go to *C:\Users\*
	1. Rename the user's current profile folder to have `.old` at the end
		* `hsimpson` would become `hsimpson.old`
1. Backup and delete the registry entries
	1. Navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList`
		1. Look through the different entries looking for the *SID* of the user you are rebuilding
			* Use *Profile Image Path* to see the username associated with the *SID*
			* When you find it, right click and export the key to the desktop
			* Note the last four digits of the *SID* before you delete it
			* Export and delete the folder *containing* the *Profile Image Path* entry
	1. Navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Current Version\ProfileGuid`
		1. Look through the different entries looking for the *SID* of the user you are rebuilding
			* you don't have *Profile Image Path* this time; this is why you needed to note the last four digits in the last step. I bet you wish you'd've listened to me now.
			* If you didn't listen to me and note or forgot, you can refer to the exported file on the desktop if you open it in *Notepad*
			* Make sure to export this one too prior to deleting it
1. Reboot again
1. Log in as the user
1. Log out and log back in as the admin again
	1. Open the new profile folder and old profile folder side by side
	1. Copy anything relevant from the old profile to the new one
		* Do **NOT** copy *AppData*! This is likely the source of whatever issues you are rebuilding for!
		* You may *selectively* copy from *AppData* for software settings that you know aren't in conflict
		* Example: Chrome user data folder may be copied `C:\Users\username\AppData\Local\Google\Chrome\User Data`
		* Sticky notes are located at `C:\Users\username\AppData\Roaming\Microsoft\Sticky Notes`
	1. When finished, leave the *.old* profile for at least a month or two before deleting (always the potential for needing to recover more data)
1. Log back in as user
1. Confirm settings like taskbar icons, network drives, printers
