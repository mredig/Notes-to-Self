<!-- permalink: 338e8d48346401a118cd50d6b0838043 DO NOT DELETE OR EDIT THIS LINE -->
# Let's Encrypt Setup

1. Download and set up *certbot* (Only do this once)
	* `wget https://dl.eff.org/certbot-auto`
	* Suggested placement in `/opt/letsencrypt/`
1. Run *certbot-auto*
	1. To renew:
		* `./certbot-auto certonly --force-renew --manual -d domain.name.com`
	1. To create a new request:
		* `./certbot-auto certonly --manual`
	1. If you are running from a webserver on the public internet, you can drop the `--manual` and it will handle much of the process automatically. If you are uncomfortable with the script modifying your webserver conf files, you might wish to retain the `--manual` flag
	1. Answer prompts accordingly
1. It will need to verify ownership of domain (this is only if you are running `--manual` and the internet does't have direct access to the machine)
	1. On another webserver accessible via the internet, navigate to the root folder that is accessible via the domain you are testing (you may need to configure dns to point to this server)
	1. Run the *printf* statement *certbot* requests
	1. Finish the cert update
