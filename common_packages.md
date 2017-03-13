# Common Packages

Most of these will just work following `sudo apt-get install`, but some will have other manual dependencies. I will try to note where, but it will inevitably get out of date.

* Apache
	* `apache2`
* Borg
	* `borgbackup` - requires *stretch* on debian
* BSD-Mailx
	* `bsd-mailx`
		* configure with `dpkg-reconfigure exim4-config`
* Fail2Ban
	* `fail2ban`
* Fuse
	* `fuse`
* HFS Filesystem support
	* `hfsprogs`
* MariaDB
	* `mariadb-server`
* PHP
 	* `php5`
	* `php5-mysqli`
	* `php7.0` - requires *stretch* on debian
	* `php7.0-mbstring php7.0-mysql php7.0-curl`
* Samba
	* `samba`
* Samba fstab client
	* `cifs-utils`
* UFW
	* `ufw`
	* `gufw` - gui
* Unattended Upgrades
	* `unattended-upgrades`
* VNC
	* `x11vnc vnc4server`
