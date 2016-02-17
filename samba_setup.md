# Samba Setup on Linux

1. run updates
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
2. sudo apt-get install 
	* samba
3. create samba users (I believe they are the same user as local login, but just use a different password for auth, which needs setting here)
	* `sudo smbpasswd -a <username here>`
4. Set permissions to any files and folders you want to share to be correct to the user
5. setup shares in the /etc/samba/smb.conf with the following syntax - I put it after the Authentication section and before the Domains section
	* `[<share_name>]`
	`path = /path/to/folder/to/share`
	`valid users = <user_name>`
	`read only = no`
	* note that it MAY be important to have an blank line between each line 