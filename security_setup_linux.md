# Linux Security Prep List

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
* [Create *ssh key auth*](ssh_keyfile.md)
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
