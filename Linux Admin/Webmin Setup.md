# Installing Webmin

1. Download webmin from the official site:
	* `wget http://www.webmin.com/download/deb/webmin-current.deb`
1. Install
	1. `dpkg --install webmin-current.deb`
		* It will error here which is rectified in the next step
	1. `sudo apt-get install -f`
1. Set firewall to allow access over port 10000
	* `ufw allow from 192.168.1.1/24 to any port 10000` 
