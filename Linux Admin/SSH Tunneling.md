# SSH Tunneling

* ssh tunnel
	* `ssh -L [localForwardPort]:[targetAddress]:[targetPort] [sshServerToTunnelThrough]`
	* example:
		* `ssh -L 9001:google.com:80 ssh.yourserver.net` (not a real ssh server)
		* Navigate to `localhost:9001` in your browser to get google.com tunneled through ssh.yourserver.net
