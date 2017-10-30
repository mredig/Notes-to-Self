<!-- permalink: 6e4cef2ff7c2f2229cd6975c1cc265e4 DO NOT DELETE OR EDIT THIS LINE -->
# RPi Print Server

1. `sudo apt update && sudo apt upgrade -y`
1. If the printer is USB, you can use `lsusb` to confirm the printer is connected
1. Install *CUPS*
	* `sudo apt install cups`
	* It might be an exception if there are driver for the RPi Linux (I believe it is a binary file that would need to be compiled for the RPi)
	* If you will be using with Windows clients, add *samba* to the package list to install
1. Add your user to the printer admin group
	* `sudo usermod –a –G lpadmin your_username`
1. Before you can setup the printer, you need to edit the conf file:
	* `nano -B /etc/cups/cupsd.conf`
	* It should look similar to this after editing:
		* Don't include the comments as I don't know if these are actually comments for the config file

				Listen localhost:631
				Listen /var/run/cups/cups.sock
				Listen 192.168.1.2:631 ## whatever your Pi IP is

				Browsing On
				BrowseLocalProtocols dnssd
				DefaultAuthType Basic
				WebInterface Yes
				<Location />
				  Order allow,deny
				  Allow localhost
				  Allow 192.168.1.* ## whatever your IP scheme is
				</Location>
				<Location /admin>
				  Order allow,deny
				  Allow localhost
				  Allow 192.168.1.* ## whatever your IP scheme is
				</Location>

1. After editing, restart CUPS
	* `sudo service cups restart`
1. Open a browser and navigate to the IP of the Pi on port *631*
1. Under the *Administration* tab you should be able to add a printer after logging on with your Pi user credentials
	* If drivers exist that work for the printer, great! If not, set the drivers to *Raw* and let the clients install their own drivers
1. If you're not using Windows clients, you're done apart from setting up the printers on the client computers! If you are, *samba* needs a bit of tweaking yet...
1. Open the samba settings:
	* `nano -B /etc/samba/smb.conf`
1. In the print section, match these settings:

	```
	# CUPS printing.  See also the cupsaddsmb(8) manpage in the
	# cupsys-client package.
	printing = cups
	printcap name = cups
	[printers]
	comment = All Printers
	browseable = no
	path = /var/spool/samba
	printable = yes
	guest ok = yes
	read only = yes
	create mask = 0700

	# Windows clients look for this share name as a source of downloadable
	# printer drivers
	[print$]
	comment = Printer Drivers
	path = /usr/share/cups/drivers
	browseable = yes
	read only = yes
	guest ok = no
	```

1. Restart samba and setup client computers!
	* `sudo /etc/init.d/samba restart`



[reference](http://www.makeuseof.com/tag/make-wireless-printer-raspberry-pi/)
