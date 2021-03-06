<!-- permalink: 73fad25d8760dac03807a9d147a9663c DO NOT DELETE OR EDIT THIS LINE -->
# Setting up VNC on Linux

## X11 VNC (recommended)

1. Update
	* `sudo apt-get update && sudo apt-get upgrade -y`
1. Install server
	* `sudo apt-get install x11vnc vnc4server`
1. Start server for one session
	* `sudo x11vnc -display :0` - the same display as is shown on the server's local monitor.
1. Possible arguments
	* `-auth guess` - easy mode
	* `-auth /var/gdm/:0.Xauth`
		* run `ps wwaux | grep auth` and look for the string after `-auth` to get the actual location of the xauth file
	* [this forum post](https://ubuntuforums.org/showthread.php?t=363236) might be helpful in turning this into a service to run in the background and not just manually run. However, make sure you up the security first!



## XTightVNC (not recommended)

### Single Use Scenario
1. Do the usual
	* `sudo apt-get update && sudo apt-get upgrade -y`
1. Install tightVNC server
	* `sudo apt-get install tightvncserver`
1. Do a first run on the vnc server
	* `tightvncserver`
1. Run the server:
	* `vncserver :0 -geometry 1920x1080 -depth 24`

### Start at boot
1. Create a file at `/etc/init.d/`
	* `sudo nano /etc/init.d/vncboot`
1. Paste in the following text:

		#!/bin/sh
		### BEGIN INIT INFO
		# Provides: vncboot
		# Required-Start: $remote_fs $syslog
		# Required-Stop: $remote_fs $syslog
		# Default-Start: 2 3 4 5
		# Default-Stop: 0 1 6
		# Short-Description: Start VNC Server at boot time
		# Description: Start VNC Server at boot time.
		### END INIT INFO

		USER=root
		HOME=/root

		export USER HOME

		case "$1" in
		start)
		echo "Starting VNC Server"
		#Insert your favoured settings for a VNC session
		/usr/bin/vncserver :0 -geometry 1280x800 -depth 16 -pixelformat rgb565
		;;

		stop)
		echo "Stopping VNC Server"
		/usr/bin/vncserver -kill :0
		;;

		*)
		echo "Usage: /etc/init.d/vncboot {start|stop}"
		exit 1
		;;
		esac

		exit 0
1. Save and exit (Ctrl-o and Ctrl-x)
1. Set permissions
	* `sudo chmod 755 /etc/init.d/vncboot`
1. Do this thing
	* `sudo update-rc.d /etc/init.d/vncboot defaults`
	* use relative paths if it errors
1. reboot and connect!
