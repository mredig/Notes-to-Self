<!-- permalink: 62d1b9fc3ec8ea9175c30cc735d66654 DO NOT DELETE OR EDIT THIS LINE -->
# SSH Tunneling

* ssh tunnel
	* `ssh -L [localForwardPort]:[targetAddress]:[targetPort] [sshServerToTunnelThrough]`
	* example:
		* `ssh -L 9001:google.com:80 ssh.yourserver.net` (not a real ssh server)
		* Navigate to `localhost:9001` in your browser to get google.com tunneled through ssh.yourserver.net
