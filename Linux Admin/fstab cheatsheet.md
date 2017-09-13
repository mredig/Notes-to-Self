<!-- permalink: 1355ea1922196e420d8c93473a6fb6ac DO NOT DELETE OR EDIT THIS LINE -->
# Linux FSTab Cheatsheet

Mount via UUID
* get UUID
	* `sudo blkid /dev/sdxy`
* enter into `/etc/fstab`
	* `UUID=[uuidnobrackets] /mount/point ext4 `
