<!-- permalink: aeeb1295c2afdaa243d5e829caeb64e6 DO NOT DELETE OR EDIT THIS LINE -->
# Speed Testing Specific Device (specifically UniFi)

Note that this method isn't fully verified for integrity.

1. *ssh* into the device
	* you may not be able to ssh directly into the device, and instead might need to tunnel through other devices on the network. For example, a *UniFi Firewall* won't be directly accessible through the WAN connection, but if you set up port forwarding to another device on the network (port 22) you can *ssh* into that secondary device and then *ssh* back to the firewall.
	* you can find the credentials for the admin user in the UniFi portal. Select the site you're testing, click on the *Settings* gear icon in the bottom left of the page, and on the *Site* page there will be an entry called *Device Authentication*. This will be the username and password to use for *ssh*.
	* `ssh [ipaddress] -l admin`
1. UniFi devices have at least two distinct OSes. One has `wget` and the other has `curl` - they perform similar functions, but the commands vary a bit.
	* `curl http://website.com/largefile.zip > /dev/null`
	* `wget --output-document=/dev/null http://website.com/largefile.zip`
1. The download speed will be displayed as *BYTES per second* (most speeds are measured as *BITS per second*). Google can help translate


### upload testing

* you'll have to use `scp` probably
* `scp /dev/random user@remoteserver.com:/dev/null`
* download the zip file at least partially to run the upload
	* remove it afterwards
