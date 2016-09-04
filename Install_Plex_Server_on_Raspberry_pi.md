# Install Plex Media Server on Raspberry Pi

1. run updates
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
1. Possibly run dist upgrade
  * `sudo apt-get update && sudo apt-get dist-upgrade  `
1. Install some dependencies
	* `sudo apt-get install apt-transport-https -y --force-yes  `
1. Add a required auth key
  * `wget -O - https://dev2day.de/pms/dev2day-pms.gpg.key  | sudo apt-key add -`
  * `echo "deb https://dev2day.de/pms/ jessie main" | sudo tee /etc/apt/sources.list.d/pms.list  `
1. Update again
  * `sudo apt-get update`
1. Install the media server:
  * `sudo apt-get install -t jessie plexmediaserver -y`
1. Reboot:
  * `sudo reboot`
