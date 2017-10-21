# Linux VLAN Interface Configuration

1. If not already installed, install:
	* `apt install vlan`
1. Load module
	* `modprobe 8021q`
1. Create VLAN interface on parent interface:
	* if *eth0* is where the physical connection resides and connecting to VLAN ID *7*:
		* `vconfig add eth0 7`
1. Set IP and etc as you would for any other interface. This interface will now be referred to as `eth0.7`
1. If you need to make this permanent...
	* `echo "8021q" >> /etc/modules`
		* might be debian specific
	* and add something like this to `/etc/network/interfaces`
	```
	auto eth0.7
	iface eth0.7 inet static
		address 192.168.15.8
		netmask 255.255.255.0
		vlan-raw-device eth0
	```
