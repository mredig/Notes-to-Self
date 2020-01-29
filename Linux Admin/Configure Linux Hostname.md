<!-- permalink: 9909f0cf846591d7e4df2348f1350ce8 DO NOT DELETE OR EDIT THIS LINE -->
# Configure Linux Hostname

### Clarifying Terminology

In the url `www.sitename.com`:
* `www` is the subdomain
	* subdomains *can* have their own subdomains
* `sitename` is the domain name
* `com` is the TLD or *top level domain*
* `www.sitename.com` is the FQDN or `Fully Qualified Domain Name`

1. Set up your server's hostname
	* edit the file `/etc/hostname`. The entire contents of the file consists of JUST your hostname, which frequently matches the subdomain of your site.
1. Set up your server's hostfile:
	* the first line will typically be `127.0.0.1   localhost`
	* add/edit the line below `127.0.1.1   [FQDN_no_brackets] [hostname_no_brackets]`