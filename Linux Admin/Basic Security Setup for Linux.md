<!-- permalink: c716ef85197d7b5aeb5db8a7a1bd58a9 DO NOT DELETE OR EDIT THIS LINE -->
# Linux Security Prep List

A scripted implementation of this advice can be found in the [assistance scripts](https://github.com/mredig/assistant_scripts) repo.

* Automatic Upgrades
	* install [unattended upgrades](https://wiki.debian.org/UnattendedUpgrades)
	* `apt-get install unattended-upgrades`
		* configure at `/etc/apt/apt.conf.d/50unattended-upgrades`
		* RPi
			* uncomment line `"o=Raspbian,n=jessie";`
			* uncomment and set mail `Unattended-Upgrade::Mail "he@ho.hum";`
				* will need `bsd-mailx` installed and configured (see other doc)
* Add a limited user account
	* `adduser example_user`
	* `adduser example_user sudo`
* Remove default user account (if applicable eg pi)
	* `deluser --remove-home <username>`
* [Create *ssh key auth*](permalink.php?perma=16d5905a76daf3851e4d3eed5bdb1fe4)
* ssh config settings */etc/ssh/sshd_config*
	* `PermitRootLogin no`
	* `PasswordAuthentication no`
	* `AddressFamily inet` for IPv4 listening only
	* `AddressFamily inet6` for IPv6
	* `sudo service ssh restart` restart ssh afterwards
* *Fail2Ban* if you can get it to work?
* remove unused network services
	* `sudo netstat -tulpn` (part of *net-tools* package)
* setup iptables/ufw
	* ufw is a frontend for iptables
	* `apt-get install ufw gufw` (ufw is command line, gufw is gui)
	* have needed to reboot every time I installed this so far before it'll work
	* some useful commands:
		* `ufw status`
		* `ufw help`
		* `ufw allow 22`
			* **must be run before enabling ufw if you are connected via ssh**
			* replace 22 with port number for other services (refer to the earlier netstat command)
		* `ufw allow from 192.168.1.0/24 to any port 137` #local samba1
		* `ufw allow from 192.168.1.0/24 to any port 445` #local samba2
		* `ufw enable`
