<!-- permalink: 63170e68fd3123fe4eb6608bbf09cf6a DO NOT DELETE OR EDIT THIS LINE -->
# Email/Webserver With Hestia


### Prerequisite Checklist
* make sure reverse dns is configured for your server (the hostname step below has a bit more info)
	* smtp servers do not like when this is not configured
* (optional?) make a new dns entry pointed to the same A record (or CNAME) of the FQDN and append `mail` as a subdomain to the front

### Install
1. Start with a fresh install of a supported linux variant (see the download link for a list)
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
1. Perform basic security modifications (change password, don't operate as admin, etc)


### Set up DNS Cluster
1. At some point, ideally before this, you'll want to set your DNS glue records on whatever domain your servers will be on.
1. On a second server, the one destined to be a DNS slave, again start with a few install of a supported linux variant
1. Download and install with the following options:
	* `bash hst-install.sh -v no -j no -m no -x no -t no`
	* This will not install ftp/email/mysql/etc as they are uneccessary for DNS
1. Follow prompts just like the first section
1. Reboot when prompted
1. Perform basic security modifications (change password, don't operate as admin, etc)
1. Create a new user on the slave server called `dns-cluster`
	* details beyond the name username do not matter, but it's probably wise to leave ssh access to `nologin`
	* Make sure the password is secure though
1. On your master server, from an admin command prompt, run 
	* `v-add-remote-dns-host [slaveFQDNNoBrackets] [slaveControlPanelPort] admin [slaveAdminPasswordNoBrackets]`
1. You can now confirm through the slave web control panel that dns zones are syncing over. (log into the `dns-cluster` user to view)