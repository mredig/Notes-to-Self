<!-- permalink: 1225962ec805b532e8a086f737c6c428 DO NOT DELETE OR EDIT THIS LINE -->
# UniFi Cheat Sheet

#### USG ssh Cheats
* username and password:
	* ubnt
* commands
	* `unifi set-inform http://unifiController:8080/inform`
	* `unifi set-inform http://127.0.0.1:8080/inform`
	* show current firmware
		* `unifi info`
		* OR
		* `show system image`
	* upgrade firmware
		1. `add system image http://dl.ubnt.com/unifi/firmware/UGW3/4.3.11.4852825/UGW3.v4.3.11.4852825.tar`
		2. `reboot`
