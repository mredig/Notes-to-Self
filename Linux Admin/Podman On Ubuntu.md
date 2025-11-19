<!-- permalink: 566deedd03c6b0736c9a942ba92f2f81 DO NOT DELETE OR EDIT THIS LINE -->
# Podman on Ubuntu

(disclaimer - i THINK it's unique to ubuntu (on vultr?) deployments, but it may not be)

* When there's container <-> container dns issues, the default ufw config can block it
	* `ufw allow in on podman+`
	* ai explanation:
		It does **NOT** allow external traffic from the internet into your containers. That's still controlled by:
		1. Your explicit port mappings in compose (`ports: - 80:80`)
		2. UFW rules for your main interfaces (eth0, etc.)
		
		**Traffic flow:**
		- **External → Host**: Controlled by UFW rules on your main interface (eth0/ens0/whatever)
		- **Host → Containers**: Goes through podman's NAT rules
		- **Container ↔ Container**: Goes through podman1 interface ← **This is what we're allowing**
		- **Container → Gateway (DNS)**: Goes through podman1 ← **This too**
		
		So `ufw allow in on podman+` only allows traffic that's already inside the podman network space. It won't let random internet traffic reach your containers.
