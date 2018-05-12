<!-- permalink: e9c088cd827925ff4b9ae26e44b0cb73 DO NOT DELETE OR EDIT THIS LINE -->
# Linux UniFi Controller configuration


1. Install netstat to check open ports (optional)
	* `apt install net-tools -y`
1. Download unifi (version 5.6.19 here, go [here](https://www.ubnt.com/download/unifi) for almost latest, or [here](https://community.ubnt.com/t5/UniFi-Updates-Blog/bg-p/Blog_UniFi) for latest)
	* `wget https://dl.ubnt.com/unifi/5.6.19/unifi_sysvinit_all.deb`
1. Run install
	1. `dpkg -i unifi_sysvinit_all.deb`
	1. `apt install -fy`
1. Go to `ipaddress.url:8080` and finish setup
