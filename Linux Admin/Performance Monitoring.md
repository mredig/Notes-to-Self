<!-- permalink: 07a5b0144a7e55b0422d718812a91309 DO NOT DELETE OR EDIT THIS LINE -->
# System Performance Monitoring

* centos
	* install `sysstat`
	* `service sysstat start`
	* `chkconfig sysstat on`
	* logs located in `/var/log/sa/`


* debian:
	1. should already be installed
	1. `nano /etc/default/sysstat`
	 	* make sure it says `ENABLED="true"`
	1. `nano /etc/cron.d/sysstat`
		* change `5-55/10 * * * * ...` to
		* `*/2 * * * * ...`
	1. `service sysstat restart`
	1. logs are located in */var/log/sysstat/*



* `sar -r` (ram)
* `sar -n ALL` (network)
