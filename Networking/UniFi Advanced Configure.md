# UniFi Advanced Configure

This might be specific to the USG 3P, but I assume works on other devices, at least gateways.

1. `ssh` into the device
	* Optional: `sudo su` - at least I think it's optional
2. `configure`
3. run your configuration
4. run `mca-ctrl -t dump-cfg` (`> config.json` if you want to save the file) to get the complete configuration.
5. extract the relevant parts of the json and migrate to a new file named `config.gateway.json` placed in `/path/to/config/sites/[siteid]/config.gateway.json` on the controller.


#### For example, setting up OpenVPN with advanced settings like such:

1. `configure`
1. run the following configuration commands (omit the comments): 

	```
	set interfaces openvpn vtun0 mode site-to-site
	set interfaces openvpn vtun0 local-address 10.0.100.2 # this is a newly created address for THIS device on the vpn network
	set interfaces openvpn vtun0 remote-address 10.0.100.1 # this is an address for the server device on the vpn network
	set interfaces openvpn vtun0 shared-secret-key-file "/config/auth/secretfile" # shared private key file - will need to be saved separately from the config json file - use ssh
	set interfaces openvpn vtun0 openvpn-option "--dev tun"
	set interfaces openvpn vtun0 openvpn-option "--persist-key"
	set interfaces openvpn vtun0 openvpn-option "--persist-tun"
	set interfaces openvpn vtun0 openvpn-option "--cipher AES-256-CBC"
	set interfaces openvpn vtun0 openvpn-option "--auth SHA512"
	set interfaces openvpn vtun0 openvpn-option "--resolv-retry infinite"
	set interfaces openvpn vtun0 openvpn-option "--remote remoteHostAddress 1194 udp" # replace `remoteHostAddress` with the IP or url of the host. 1194 is the port that the server is listening to
	set interfaces openvpn vtun0 openvpn-option "--route 10.0.69.0 255.255.255.0" # this tells openvpn that anything in the `10.0.69.0/24` subnet is to be routed onto the openvpn network
	set interfaces openvpn vtun0 openvpn-option "--user nobody"
	set interfaces openvpn vtun0 openvpn-option "--group nogroup"
	```

1. to check your work, you can run `show interfaces openvpn vtun0`
1. If you make a mistake or otherwise need to exit without saving, run `exit discard`
1. You can now either
	* Apply the settings directly (which would likely get wiped out on the next provision)
		1. `commit` (applies the settings)
		2. `save`
		3. `exit`
	* use the `mca-ctrl -t dump-cfg` (see above) method to save to the network controller and deploy your changes
