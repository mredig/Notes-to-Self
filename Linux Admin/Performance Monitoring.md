<!-- permalink: 07a5b0144a7e55b0422d718812a91309 DO NOT DELETE OR EDIT THIS LINE -->
# System Performance Monitoring

* centos
	* install `sysstat`
	* `service sysstat start`
	* `chkconfig sysstat on`
	* logs located in `/var/log/sa/`
	* immediate results:
		* `sar -r` (ram)
		* `sar -n ALL` (network)
