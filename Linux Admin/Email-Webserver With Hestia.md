<!-- permalink: 63170e68fd3123fe4eb6608bbf09cf6a DO NOT DELETE OR EDIT THIS LINE -->
# Email/Webserver With Hestia


### Install
1. Start with a fresh install of a support linux variant (see the download link for a list)
1. Configure your [hostname](/permalink.php?perma=9909f0cf846591d7e4df2348f1350ce8)
1. [Download](https://www.hestiacp.com) the hestia installer to the server
1. Run the installer (as root - not sudo)
	* If you want to customize the install, you can find the [options here](https://docs.hestiacp.com/getting_started/all_installation_options.html), but the defaults are very sane and cover the needs of a personal web/email server (webserver/email server/spam filter/ftp/firewall/etc).
1. After checking some things, it will likely ask you if you want to remove `ufw` to be reinstalled (especially on Ubuntu since that comes preinstalled), choose yes
1. At the prompt, confirm you want to install
	* enter the email address of the admin (not to be created, but to be contacted by)
	* confirm the FQDN is correct
1. A username and password will be generated for you. Take note of these as you will need them to log in to the web console.
1. Reboot when prompted
