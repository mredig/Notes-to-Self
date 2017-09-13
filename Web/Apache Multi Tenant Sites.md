<!-- permalink: e280a5125761d2d1cb6549b6ff73832f DO NOT DELETE OR EDIT THIS LINE -->
# Apache Multi Tenant Sites

1. Navigate to `/etc/apache2/sites-available/`
1. Copy `000-default.conf` to `sitename.com.conf` and use as a template
1. Edit information in there to be relvant to the new site you're setting up
1. Add these lines to identify the information for the virtual host:
	* `ServerName sitename.com`
	* `ServerAlias www.sitename.com`
	* here is a good sample template

			<VirtualHost *:80>
				ServerName sitename.com
				ServerAlias www.sitename.com

				ServerAdmin webmaster@sitename.com
				DocumentRoot /var/www/sitename.com/html
				ErrorLog ${APACHE_LOG_DIR}/error.log
				CustomLog ${APACHE_LOG_DIR}/access.log combined
			</VirtualHost>

			<VirtualHost *:443>

				ServerName sitename.com
				ServerAlias www.sitename.com

				ServerAdmin admin@test.com
				DocumentRoot /var/www/sitename.com/html

				ErrorLog ${APACHE_LOG_DIR}/error-sitename.com.log
				CustomLog ${APACHE_LOG_DIR}/access-sitename.com.log combined

				SSLEngine On
				SSLCertificateFile /path/to/cert/sitename.crt
				SSLCertificateKeyFile /path/to/key/sitename.key

			</VirtualHost>

1. Run `a2ensite` to enable the virtual host (requires admin)
	* `a2ensite sitename.com.conf`
1. Restart apache
	* `service apache2 restart`



* [reference](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts)
