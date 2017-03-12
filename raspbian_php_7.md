# Raspbian PHP 7

 1. Add *stretch* to apt sources:
 	* `sudo nano /etc/apt/sources.list`
	* `deb http://mirrordirector.raspbian.org/raspbian/ stretch main contrib non-free rpi`
		* I personally prefer the leaseweb mirror as of late as it seems faster and more reliable.
			* `http://mirror.us.leaseweb.net/raspbian/raspbian`
1. Set apt preferences to prefer *stable* over *stretch*
	* `sudo nano /etc/apt/preferences`


			Package: *
			Pin: release n=jessie
			Pin-Priority: 600


1. Update...
	* `sudo apt-get update`
1. Install *PHP 7* specifying that it comes from *stretch*
	* `sudo apt-get install -t stretch php7.0`
	* optional: other useful packages: `php7.0-mbstring php7.0-mysql php7.0-curl`
1. Confirm *PHP* version
	* `php -v`
