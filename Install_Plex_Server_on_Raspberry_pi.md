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
1. Configure server from web interface (another computer on the network would be best) by using port *32400* in url formatted like this:
  * `hostname:32400/web`


* [Reference](https://www.element14.com/community/community/raspberry-pi/raspberrypi_projects/blog/2016/03/11/a-more-powerful-plex-media-server-using-raspberry-pi-3)

### Maintenance

The service is named *plexmediaserver* so you can use commands like

	sudo service plexmediaserver start
	sudo service plexmediaserver stop
	sudo service plexmediaserver status


UFW Settings

1. Create file `/etc/ufw/applications.d/plexmediaserver`
1. insert Contents

		[PlexMediaServer]
		title=Plex Media Server
		description=This opens up PlexMediaServer for http (32400), upnp, and autodiscovery.
		ports=32469/tcp,32413/udp,1900/udp,32400/tcp,32412/udp,32410/udp,32414/udp

1. `ufw allow plexmediaserver`
1. `ufw allow Samba`
