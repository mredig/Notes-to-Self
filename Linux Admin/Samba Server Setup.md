<!-- permalink: 13ea28a62a780d8775a083c569c94323 DO NOT DELETE OR EDIT THIS LINE -->
# Samba Setup on Linux

1. run updates
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
2. Install it
	* `sudo apt-get install samba`
3. create samba users (I believe they are the same user as local login, but just use a different password for auth, which needs setting here)
	* `sudo smbpasswd -a <username here>`
4. Set permissions to any files and folders you want to share to be correct to the user
5. setup shares in the `/etc/samba/smb.conf` with the following syntax - I put it in the *Share Definitions* section

		[<share_name>]
		comment = description
		path = /path/to/folder/to/share
		valid users = <user_name>
		read only = no
        create mask = 755
        directory mask = 755
        browseable = yes

	* this can be useful if you need to modify permissions that are written:
		* `force user = [usernameNoBrackets]`

6. restart the samba services
	* `sudo /etc/init.d/samba restart`
7. If you have a firewall setup, open ports `137` and `445`
