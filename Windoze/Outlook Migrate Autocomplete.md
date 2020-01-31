<!-- permalink: dadb9cf4381f9a36351f450398a0f3f3 DO NOT DELETE OR EDIT THIS LINE -->
# Outlook Migrate Autocomplete

##### Pre 2010 Versions of Outlook

1. Find an *.nk2* file in the folder *Drive:\Documents and Settings\Username\Application Data\Microsoft\Outlook* or *Drive:\Users\Username\AppData\Roaming\Microsoft\Outlook*
1. Place the recovered *.nk2* file in the folder `%appdata%\Microsoft\Outlook`
	* Note: The .nk2 file must have the same name as your current Outlook 2010 profile. By default, the profile name is "Outlook." To check the profile name, follow these steps:
		1. Click Start, and then click *Control Panel*.
		1. Double-click Mail.
		1. In the Mail Setup dialog box, click *Show Profiles*.
1. If migrating to 2007, you're done, if not...
1. Click Start, and then click Run.
1. In the Open box, type `outlook.exe /importnk2`, and then click *OK*. This should import the .nk2 file into the Outlook 2010 profile.

#### 2010 and Later

1. Make sure Outlook is closed.
1. From the old profile, recover the file that roughly matches `Drive:\Users\USERNAME\AppData\Local\Microsoft\Outlook\RoamCache\Stream_Autocomplete_AAAAAAAAAAAA`
	* If this is migrating from a different Outlook profile on the same computer, there are probably two files that match this pattern - the larger filesize/older modification date is likely the the one you want to recover
1. COPY that file to the same location on the new system, twice.
1. There is likely a file matching that same pattern here already - make a copy of it.
1. There should now be at least four of these files:
	* `Stream_Autocomplete_AAAAAAAAAAAA`
	* `Stream_Autocomplete_AAAAAAAAAAAA - Copy`
	* `Stream_Autocomplete_BBBBBBBBBBBB`
	* `Stream_Autocomplete_BBBBBBBBBBBB - Copy`
1. Copy the (actual) name of `Stream_Autocomplete_BBBBBBBBBBBB`, delete it, then rename `Stream_Autocomplete_AAAAAAAAAAAA`, pasting the one you just copied into it.
1. Open Outlook
1. If it worked, you're gg. If not, repeat the copy/rename step again. (I usually have to do it twice)
	* Make sure to **ALWAYS** keep a backup of the original `Stream_Autocomplete_AAAAAAAAAAAA` you recovered
