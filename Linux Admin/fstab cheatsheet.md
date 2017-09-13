# Linux FSTab Cheatsheet

Mount via UUID
* get UUID
	* `sudo blkid /dev/sdxy`
* enter into `/etc/fstab`
	* `UUID=[uuidnobrackets] /mount/point ext4 `
