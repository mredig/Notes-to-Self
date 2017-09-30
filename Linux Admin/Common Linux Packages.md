<!-- permalink: 6fa7f3401cb83baf255fc5fcbb202074 DO NOT DELETE OR EDIT THIS LINE -->
# Common Packages

Most of these will just work following `sudo apt-get install`, but some will have other manual dependencies. I will try to note where, but it will inevitably get out of date.

* Apache
	* `apache2`
* Borg
	* `borgbackup` - requires *stretch* on debian
* BSD-Mailx
	* `bsd-mailx`
		* configure with `dpkg-reconfigure exim4-config`
* DNSUtils (including `dig`)
	* `dnsutils`
* Fail2Ban
	* `fail2ban`
* Fuse
	* `fuse`
* HFS Filesystem support
	* `hfsprogs`
* MariaDB
	* `mariadb-server`
* PHP
	* `php`
	* `php-mbstring php-mysql php-curl`
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
