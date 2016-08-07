# Setting up VNC on Linux

### Single Use Scenario
1. Do the usual 
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
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