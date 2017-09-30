<!-- permalink: 97f703b7fb7623363cdf46bf23bf379b DO NOT DELETE OR EDIT THIS LINE -->
# Setup an Email/Webserver/Jabber/DNS with ISPConfig On Debian 9

Note that this has not been proofread or double checked, but should be good

1. Confirm hostname is correct:
	1. `nano /etc/hosts`
		* It should look something like this, if the server name is *controlpanel* and the domain name is *yourdomain.com*:

			```
			127.0.0.1	localhost
			[localMachineIP - noBrackets]	controlpanel.yourdomain.com controlpanel

			# The following lines are desirable for IPv6 capable hosts
			::1     localhost ip6-localhost ip6-loopback
			ff02::1 ip6-allnodes
			ff02::2 ip6-allrouters

			```

	1. `nano /etc/hostname`
		* it should simply read the server name (`controlpanel` from the above example)
	1. reboot the server
	1. confirm:
		* `hostname`
		* `hostname -f`
1. Change default shell
	* `dpkg-reconfigure dash`
		* answer *no* to using dash as the default system shell
		* ISPconfig relies on bash
1. Make sure you have *contrib non-free* tagged onto your current sources:
	* should look like (with server being whatever your current server is)

		```
		# deb http://server/debian/ stretch main
		deb http://server/debian/ stretch main contrib non-free
		deb-src http://server/debian/ stretch main contrib non-free
		deb http://security.debian.org/debian-security stretch/updates main contrib non-free
		deb-src http://security.debian.org/debian-security stretch/updates main contrib non-free
		```

1. make sure to update packages before proceeding:
	* `apt update && apt upgrade -y`
1. Install the following packages (`apt install ...` ... yes it's a doozy)
	* `ssh openssh-server nano dnsutils ntp postfix postfix-mysql postfix-doc mariadb-client mariadb-server openssl getmail4 rkhunter binutils dovecot-imapd dovecot-pop3d dovecot-mysql dovecot-sieve dovecot-lmtpd sudo amavisd-new spamassassin clamav clamav-daemon zoo unzip bzip2 arj nomarch lzop cabextract apt-listchanges libnet-ldap-perl libauthen-sasl-perl clamav-docs daemon libio-string-perl libio-socket-ssl-perl libnet-ident-perl zip libnet-dns-perl libdbd-mysql-perl postgrey git lua5.1 liblua5.1-0-dev lua-filesystem libidn11-dev libssl-dev lua-zlib lua-expat lua-event lua-bitop lua-socket lua-sec luarocks luarocks apache2 apache2-doc apache2-utils libapache2-mod-php libapache2-mod-fcgid apache2-suexec-pristine php-pear mcrypt imagemagick libruby libapache2-mod-python memcached php-memcache php-imagick php-gettext memcached libapache2-mod-passenger php-soap php php-common php-gd php-mysql php-imap phpmyadmin php-cli php-cgi php-mcrypt php-curl php-pspell php-recode php-sqlite3 php-tidy php-xmlrpc php-xsl php-intl php-zip php-mbstring certbot php-fpm php-opcache php-apcu mailman pure-ftpd-common pure-ftpd-mysql quota quotatool bind9 dnsutils haveged webalizer awstats geoip-database libclass-dbi-mysql-perl libtimedate-perl build-essential autoconf automake libtool flex bison debhelper binutils fail2ban roundcube roundcube-core roundcube-mysql roundcube-plugins python-certbot-apache`
	* In no particular order, you will be asked the following questions about package configuration:
		* email:
			* type of mail configuration:
				* *Internet site*
			* system mail name (no brackets)
				* `hostname.domain.tld`
				* `controlpanel.yourdomain.com` in the earlier example
		* phpmyadmin (pma)
			* web server to reconfigure:
				* *apache2*
			* configure database for pma:
				* *yes*
			* pma application password
				* just hit enter
			* admin password
				* mysql root password (not set yet... will be set after everything installs, so make note of what you enter here to be used to set it to match)
		* mailman:
			* languages to support
				* choose at least one
			* missing site list
				* *ok*
1. Configure and secure MariaDB (MariaDB is a drop in replacement for MySQL):
	1. `mysql_secure_installation`
		1. change the root password:
			* *yes*
		1. make note of the password for the sql root
		1. remove anonymous users:
			* *yes*
		1. disallow remote root login:
			* *yes*
		1. remove test database:
			* *yes*
		1. reload privilege tables:
			* *yes*
	1. `nano /etc/mysql/mariadb.conf.d/50-server.cnf`
		* should look like:
			```
			[...]
			# Instead of skip-networking the default is now to listen only on
			# localhost which is more compatible and is not less secure.
			#bind-address           = 127.0.0.1

			sql-mode="NO_ENGINE_SUBSTITUTION"

			[...]
			```
	1. `echo "update mysql.user set plugin = 'mysql_native_password' where user='root';" | mysql -u root`
		* does something for PHPMyAdmin
	1. `nano /etc/mysql/debian.cnf`
		* should look like:
			```
			# Automatically generated for Debian scripts. DO NOT TOUCH!
			[client]
			host = localhost
			user = root
			password = [rootpasswordNobrackets]
			socket = /var/run/mysqld/mysqld.sock
			[mysql_upgrade]
			host = localhost
			user = root
			password = [rootpasswordNobrackets]
			socket = /var/run/mysqld/mysqld.sock
			basedir = /usr
			```
	1. `service mysql restart`
	1. if you want to confirm that it's running with networking
		* `netstat -tulpn` and look for an entry for mysqld *LISTENING* on port 3306
1. Stop *spamassassin* service (ispconfig just uses the libraries and the service is unecessary)
	1. `service spamassassin stop`
	1. `systemctl disable spamassassin`
1. Configure Postfix:
	1. `nano /etc/postfix/master.cf`
		* should look like:

			```
			[...]
			submission inet n - - - - smtpd
			 -o syslog_name=postfix/submission
			 -o smtpd_tls_security_level=encrypt
			 -o smtpd_sasl_auth_enable=yes
			 -o smtpd_client_restrictions=permit_sasl_authenticated,reject
			# -o smtpd_reject_unlisted_recipient=no
			# -o smtpd_client_restrictions=$mua_client_restrictions
			# -o smtpd_helo_restrictions=$mua_helo_restrictions
			# -o smtpd_sender_restrictions=$mua_sender_restrictions
			# -o smtpd_recipient_restrictions=
			# -o smtpd_relay_restrictions=permit_sasl_authenticated,reject
			# -o milter_macro_daemon_name=ORIGINATING
			smtps inet n - - - - smtpd
			 -o syslog_name=postfix/smtps
			 -o smtpd_tls_wrappermode=yes
			 -o smtpd_sasl_auth_enable=yes
			 -o smtpd_client_restrictions=permit_sasl_authenticated,reject
			# -o smtpd_reject_unlisted_recipient=no
			# -o smtpd_client_restrictions=$mua_client_restrictions
			# -o smtpd_helo_restrictions=$mua_helo_restrictions
			# -o smtpd_sender_restrictions=$mua_sender_restrictions
			# -o smtpd_recipient_restrictions=
			# -o smtpd_relay_restrictions=permit_sasl_authenticated,reject
			# -o milter_macro_daemon_name=ORIGINATING
			[...]
			```

	1. Configure *Mailman*
		* I don't know what this is, but apparently we need to create a first mailing list:
			1. `newlist mailman`
				* enter email of person running list:
					* enter an email, can probably be one that isn't created yet
				* initial mailman password
					* create a password i think?
				* says something about how the following lines need to be included in */etc/aliases*
			1. `nano /etc/aliases`
				* paste the previous lines in
			1. `newaliases`
			1. follow it up with `service postfix restart`
			1. `ln -s /etc/mailman/apache.conf /etc/apache2/conf-enabled/mailman.conf`
				* apparently can access things through [http://[hostname.domain.com]/cgi-bin/mailman/admin](http://[hostname.domain.com]/cgi-bin/mailman/admin) and [http://[hostname.domain.com]/cgi-bin/mailman/listinfo](http://[hostname.domain.com]/cgi-bin/mailman/listinfo)
			1. `service mailman start`
1. Configure *Metronome* for Jabber (optional)
	1. Add the following repository to apt sources:
		* `echo "deb http://packages.prosody.im/debian stretch main" > /etc/apt/sources.list.d/metronome.list`
		* `wget http://prosody.im/files/prosody-debian-packages.key -O - | sudo apt-key add -`
	1. `luarocks install lpc`
	1. `adduser --no-create-home --disabled-login --gecos 'Metronome' metronome`
	1. `cd /opt; git clone https://github.com/maranda/metronome.git metronome`
	1. `cd ./metronome; ./configure --ostype=debian --prefix=/usr`
	1. `make`
	1. `make install`

1. configure *Roundcube*
	1. `nano /etc/roundcube/config.inc.php`
		* make sure these values are set:

			```
			$config['default_host'] = 'localhost';
			$config['smtp_server'] = 'localhost';
			```
	1. `nano /etc/apache2/conf-enabled/roundcube.conf`
		* add the following line:
			* `Alias /webmail /var/lib/roundcube`
	1. Now is accessible via [http://[hostname.domain.com]/webmail](http://[hostname.domain.com]/webmail)


1. Configure *Apache*
	1. enable modules:
		* `a2enmod suexec rewrite ssl actions include dav_fs dav auth_digest cgi headers actions proxy_fcgi alias`
	1. workaround *HTTPOXY* vulnerability
		1. `nano /etc/apache2/conf-available/httpoxy.conf`
			* contents should be:

				```
				<IfModule mod_headers.c>
				    RequestHeader unset Proxy early
				</IfModule>
				```
		1. `a2enconf httpoxy`
		1. `service apache2 restart`
	1. fix PHPMyAdmin access
		1. `ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-enabled/phpmyadmin.conf`

1. Configure *PureFTPd*
	1. `nano /etc/default/pure-ftpd-common`
		* should look like:

			```
			[...]
			STANDALONE_OR_INETD=standalone
			[...]
			VIRTUALCHROOT=true
			[...]
			```
	1. `echo 1 > /etc/pure-ftpd/conf/TLS`
	1. return to use letsencrypt cert
1. Configure quota
	1. `nano /etc/fstab`
		* add `,usrjquota=quota.user,grpjquota=quota.group,jqfmt=vfsv0` to the partition with mount point of `/`
		* should look vaguely like:

			```
			/dev/sda1 / ext4 errors=remount-ro,usrjquota=quota.user,grpjquota=quota.group,jqfmt=vfsv0 0 1
			```
	1. `mount -o remount /`
	1. `quotacheck -avugm`
	1. `quotaon -avug`
1. Make *AWStats* sane
	1. `nano /etc/cron.d/awstats`
	1. comment all lines to start with `#`
1. Install *Jailkit* (This NEEDS to be done before running the isp config install!)
	1. `cd /tmp`
	1. `wget http://olivier.sessink.nl/jailkit/jailkit-2.19.tar.gz`
	1. `tar xvfz jailkit-2.19.tar.gz`
	1. `cd jailkit-2.19`
	1. `echo 5 > debian/compat`
	1. `./debian/rules binary`
	1. `cd ..`
	1. `dpkg -i jailkit_2.19-1_*.deb`
	1. `rm -rf jailkit-2.19*`
1. Configure *fail2ban*
	1. `nano /etc/fail2ban/jail.local`
		* insert following contents:

			```
			[pure-ftpd]
			enabled = true
			port = ftp
			filter = pure-ftpd
			logpath = /var/log/syslog
			maxretry = 3

			[dovecot]
			enabled = true
			filter = dovecot
			logpath = /var/log/mail.log
			maxretry = 5

			[postfix-sasl]
			enabled = true
			port = smtp
			filter = postfix-sasl
			logpath = /var/log/mail.log
			maxretry = 3
			```
	1. `service fail2ban restart`


1. Run *ISPConfig* setup
	1. `cd /tmp`
	1. `wget http://www.ispconfig.org/downloads/ISPConfig-3-stable.tar.gz`
	1. `tar -zxvf ISPConfig-3-stable.tar.gz`
	1. `cd ispconfig3_install/install/`
	1. `php -q install.php`
		* you'll be asked a series of questions. Most of them are fairly obvious, but here are the ones I've deemed questionable:
			* installation mode:
				* *standard*
			* certificate questions:
				* for the most part, these should/will be replaced with letsencrypt, so they PROBABLY don't matter? Still, try to answer them appropriately. As for the last couple questions about a challenge password and company name, you can skip those.


1. run certbot for main site
	* `certbot --apache`
1. setup cron for certbot
	* `certbot renew --apache --dry-run` (i think? - to confirm automation working)
	* `[randomMinValueNoBrackets] [randomHourValueNoBrackets] * * * /usr/bin/certbot renew --apache`
1. pure-ftpd fixes:
	1. `echo "42424 44242" > /etc/pure-ftpd/conf/PassivePortRange`
		* This sets a range on the ports than can be used for passive connections. Now that you know the port range, you can continue using your firewall to safely open ports in that range.
	1. `mkdir -p /etc/ssl/private/`
	1. `cat /etc/letsencrypt/live/[domainnobrackets]/privkey.pem /etc/letsencrypt/live/[domainnobrackets]/fullchain.pem >> pure-ftpd.pem`
	1. `/etc/init.d/pure-ftpd-mysql restart`
1. confirm the following ports are open on firewall (not comprehensive)
	* `21`
	* `22`
	* `25`
	* `53`
	* `80`
	* `110`
	* `143`
	* `443`
	* `953`
	* `993`
	* `995`
	* `42424:44242/tcp`
	* whatever you had the admin portal on (`8080` is default)


Please give credit to [this walkthrough](https://www.howtoforge.com/tutorial/perfect-server-debian-9-stretch-apache-bind-dovecot-ispconfig-3-1/) which much of this is based off of.
