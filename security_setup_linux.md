# Linux Security Prep List

* Automatic Upgrades
* Add a limited user account
	* `adduser example_user`
	* `adduser example_user sudo`
* [Create *ssh key auth*](ssh_keyfile)
* ssh config settings */etc/ssh/sshd_config*
	* `PermitRootLogin no`
	* `PasswordAuthentication no`
	* `AddressFamily inet` for IPv4 listening only
	* `AddressFamily inet6` for IPv6
	* `sudo service ssh restart` restart ssh afterwards
* *Fail2Ban* if you can get it to work?
* remove unused network services
	* `sudo netstat -tulpn` (part of *net-tools* package)
* setup iptables
	* `sudo iptables -L -nv` to list current rules
	* create file */tmp/v4* and `sudo iptables-restore < /tmp/v4`



			*filter

			# Allow all loopback (lo0) traffic and reject traffic
			# to localhost that does not originate from lo0.
			-A INPUT -i lo -j ACCEPT
			-A INPUT ! -i lo -s 127.0.0.0/8 -j REJECT

			# Allow ping.
			-A INPUT -p icmp -m state --state NEW --icmp-type 8 -j ACCEPT

			# Allow SSH connections.
			-A INPUT -p tcp --dport 22 -m state --state NEW -j ACCEPT

			# Allow HTTP and HTTPS connections from anywhere
			# (the normal ports for web servers).
			-A INPUT -p tcp --dport 80 -m state --state NEW -j ACCEPT
			-A INPUT -p tcp --dport 443 -m state --state NEW -j ACCEPT

			# Allow inbound traffic from established connections.
			# This includes ICMP error returns.
			-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

			# Log what was incoming but denied (optional but useful).
			-A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables_INPUT_denied: " --log-level 7

			# Reject all other inbound.
			-A INPUT -j REJECT

			# Log any traffic that was sent to you
			# for forwarding (optional but useful).
			-A FORWARD -m limit --limit 5/min -j LOG --log-prefix "iptables_FORWARD_denied: " --log-level 7

			# Reject all traffic forwarding.
			-A FORWARD -j REJECT

			COMMIT

	* get iptables to load config on each boot
		* `sudo apt-get install iptables-persistent`
		* answer *yes* to all
		* remove temporary rule file `sudo rm /tmp/v4`
