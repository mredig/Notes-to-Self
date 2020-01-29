# SMTP Testing with Telnet


wait for acknowledgement after each command

1. establish a conneciton
	* `telnet smtp.server.com 25`
	* or
	* `openssl s_client -debug -starttls smtp -crlf -connect smtp.server.com:25` - ssl (skip the helo step)
1. tell the remote server what your network name is
	* `helo mydomain.com`
	* or
	* `ehlo mydomain.com`
1. `mail from:<your@email.address>`
1. `rcpt to:<test@address.com>`
1. `data`
1. enter your test message, followed by `\n.\n` (newline period newline)
	* to include typical meta data, you can head your message with this kind of info:


			To: receiver@email.address
			From: sending@email.address
			Subject: this is a test

			Don't miss that line break between the header and message!


1. `quit`
