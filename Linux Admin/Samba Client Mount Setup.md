<!-- permalink: 949c09c6b4c3684121671d66f9abb5f9 DO NOT DELETE OR EDIT THIS LINE -->
# Samba Client Mount Setup on Linux

1. run updates
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
2. Install client software
	* `sudo apt-get install cifs-utils`
3. Create a credentials file
	* set permissions accordingly as this will be storing a password in plaintext
		* I used root and stored it in root home with 750 permissions
	* Plaintext file with contents like

			username=<username>
			password=<password>
			domain=<domain>

4. Add a line to /etc/fstab
	* `//<IPAddressOrHostname>/<share name>	/path/to/mount/point	cifs credentials=/path/to/credentials`
	* example: `//192.168.1.36/myshare /media/myshare cifs credentials=/home/myname/credentials/samba.credentials`
5. Make sure your fstab file is valid
 	* `mount -a` as root will mount everything in /etc/fstab
6. If you have permissions trouble, you can add this to the options on the fstab line after the credentials file using commas to separate arguments
	* `credentials=/path/to/credentials,file_mode=0664,dir_mode=0775,gid=adm`
1. Conecting to an Airport might require you to add `sec=ntlm` to the above arguments
7. This share should be mounted on every boot now
