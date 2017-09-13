<!-- permalink: e544d5373b6f3207fb72360c9860432d DO NOT DELETE OR EDIT THIS LINE -->
# Setting Up MariaDB on macOS

1. install [homebrew](http://brew.sh)
1. install MariaDB
	* `brew install mariadb`
1. initialize *mariadb* and set permissions for *phpmyadmin* access
	* `mysql -u root`
1. Then from within mysql (replace MyNewPass with actual password - note that it's cached in your home directory)

		UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
		GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'MyNewPass' WITH GRANT OPTION;
		FLUSH PRIVILEGES;

1. as of this writing, the default paths for mariadb conf files are
	* `/usr/local/etc/my.cnf`
	* files within `/usr/local/etc/my.cnf.d/`
	* `~/.my.cnf`
1. create a conf file (obviously adjust paths as necessary):
	* `cp /usr/local/Cellar/mariadb/10.1.20/support-files/my-small.cnf /usr/local/etc/my.cnf.d/my.cnf`
1. edit the new conf file:
	* `nano /usr/local/etc/my.cnf.d/my.cnf`
1. add this line....
	* `bind-address	= 0.0.0.0`
1. ... so it looks like this:

		[mysqld]
		bind-address    = 0.0.0.0
		port            = 3306
		socket          = /tmp/mysql.sock

1. install *phpMyAdmin* to your webserver to administer the mysql database
	* get it [here](https://www.phpmyadmin.net)
	* unzip, place files in server, etc
1. I did this:
	1. copy *config.sample.inc.php* to `config.inc.php`
	1. edit settings in there (I only needed what was already uncommented)
	1. use `cookie` for login mode as it will prompt you when you go to site then

			$cfg['Servers'][$i]['auth_type'] = 'cookie';
			/* Server parameters */
			$cfg['Servers'][$i]['host'] = '127.0.0.1';
			$cfg['Servers'][$i]['connect_type'] = 'tcp';

	1. it worked like that
1. Alternatively, it looks as if you can go to phpmyadminurl.com/setup and generate a conf file there, but then be sure to give it the same `config.inc.php` filename in the root directory of phpmyadmin. (easier if it works)
1. Log on through *phpmyadmin*
