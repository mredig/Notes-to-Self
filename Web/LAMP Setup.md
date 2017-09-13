<!-- permalink: 218961f9fdb953739c9858495ccd17a9 DO NOT DELETE OR EDIT THIS LINE -->
# Lamp setup on Raspbian

1. run updates
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
2. using the add/remove software option in preferences add
	* `apache2`
	* `php5`
	* `php5-mysqli`
	* mysql server
	* (note that the names are not exact)
3. Set php to display errors and integrate with mysql
	* file located at `/etc/php5/apache2/php.ini`
	* make sure lines are thus:
		* `display_errors = on`
		* `extension_dir = "/usr/lib/php5/20131226/"` (if that's not accurate, just look around in that vicinity)
	* `sudo /etc/init.d/apache2 restart`
3. setup mysql user
	* `mysql -u root`
	* now using mysql prompt
	* `update user set password=PASSWORD('this-is-password-here') where User='root';`
	* `flush privileges;`
	* `create user 'newUser'@'localhost' identified by 'password';`
		* you may want to replace "localhost" with "%" wildcard
	* `grant all on *.* to newUser@'%';` - grants permission to use all databases
4. Setup mysql remote access
	* edit /etc/mysql/my.cnf to comment line `bind-address = 127.0.0.1`
		* `sudo nano -B my.cnf` is nice for auto backing up
	* restart mysql
		* `sudo /etc/init.d/mysql restart`
5. You should now be able to connect from a remote client and manage mysql
	* check that php is able to connect with this:
		* `<?php`
		`phpinfo();`
		`?>`
