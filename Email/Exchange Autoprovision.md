<!-- permalink: a71215e708d27a32a28012ad83c44f07 DO NOT DELETE OR EDIT THIS LINE -->
# Setting up Autoprovisioning on Email Servers

## Autoprovisioning
(note that this might ONLY work for exchange/or require additional setup on the server to support this)
1. Create an *SRV* record
	* `_autodiscover._tcp` for the zone
	* `0 0 443 [serverDomainNameNoBrackets]` - entry

## SPF Record
1. Create a *TXT* record
	* `"v=spf1 ip4:[validIPNoBrackets] ip4:[optionalAdditionalIPNoBrackets] a:[optionalValidDomain-eg-google.com] ~all"`
