# Generating SSL Certificates For Apache

1. Run this as root (the key will not be password protected so you need to make sure it's limited in access) in the root home folder
1. Generate a private key:
	* `openssl genrsa -des3 -out server.key 4096`
	* it will require a password - we will be removing it shortly, just note what it is until then
1. Remove the password from the key
	* `cp server.key server.key.orig`
	* `openssl rsa -in server.key.orig -out server.key`
1. Generate a key request
	* `openssl req -new -key server.key -out server.csr`
	* it will ask for the password from earlier
1. Generate the certificate
	* `openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt`
1. Secure the files so only root can read them
	* `chmod 600 server.*`
1. Create a place for them to go if it doesn't already exist
	* `mkdir -p /etc/apache2/ssl`
1. Copy the certificate into place
	* `cp server.crt /etc/apache2/ssl/site.crt`
	* `cp server.key /etc/apache2/ssl/site.key`
1. Edit the apache virtual host conf file for the site to match something like this:


	<VirtualHost *:80>
		# The ServerName directive sets the request scheme, hostname and port that
		# the server uses to identify itself. This is used when creating
		# redirection URLs. In the context of virtual hosts, the ServerName
		# specifies what hostname must appear in the request's Host: header to
		# match this virtual host. For the default virtual host (this file) this
		# value is not decisive as it is used as a last resort host regardless.
		# However, you must set it for any further virtual host explicitly.
		#ServerName www.example.com

		ServerAdmin webmaster@localhost
		DocumentRoot /***/path

		# Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
		# error, crit, alert, emerg.
		# It is also possible to configure the loglevel for particular
		# modules, e.g.
		#LogLevel info ssl:warn

		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined

		# For most configuration files from conf-available/, which are
		# enabled or disabled at a global level, it is possible to
		# include a line for only one particular virtual host. For example the
		# following line enables the CGI configuration for this host only
		# after it has been globally disabled with "a2disconf".
		#Include conf-available/serve-cgi-bin.conf



	</VirtualHost>

	<VirtualHost *:443>
		ServerAdmin webmaster@localhost
		DocumentRoot /***/path

		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined

		SSLEngine On
		SSLCertificateFile /***/path
		SSLCertificateKeyFile /***/path
		<Location />
			SSLRequireSSL On
	#		SSLVerifyClient optional
	#		SSLVerifyDepth 1

			SSLOptions +StdEnvVars +StrictRequire
		</Location>
	</VirtualHost>


	# vim: syntax=apache ts=4 sw=4 sts=4 sr noet


1. If not already enabled, enable ssl mod
	* `a2enmod ssl`
1. Restart apache
	* `service apache2 restart`


* [reference1](http://www.akadia.com/services/ssh_test_certificate.html)
* [reference2](https://beeznest.wordpress.com/2008/04/25/how-to-configure-https-on-apache-2/)
