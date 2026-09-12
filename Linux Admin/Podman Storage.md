# Podman Storage

This is assuming initial setup - migrating an existing setup can complicate things, especially if you use volumes.

1. `nano /etc/containers/storage.conf` (if that doesn't exist yet, a template/the default is at `/usr/share/containers/storage.conf`)
2. under `[storage]`, update the locations for 
	- `graphroot` (container storage)
	- `imagestore` (image storage)
	- **!!Important!!** if the location is an external drive, make sure this is ALWAYS mounted before podman initializes!
3. reboot
