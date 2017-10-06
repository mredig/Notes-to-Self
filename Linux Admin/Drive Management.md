<!-- permalink: 1355ea1922196e420d8c93473a6fb6ac DO NOT DELETE OR EDIT THIS LINE -->
# Linux Drive Management

### Create Partitions from Command Line
1. Get a list of drives installed to identify the current device of the drive you are looking to format:
	* `fdisk -l | grep '^Disk'`
		* find the `/dev/sd*` that matches what you're trying to configure
1. `fdisk /dev/sd[driveLetterNoBrackets]`
	* might look something like `fdisk /dev/sdc`
	* *fdisk* is an interactive prompt
		* `m` for help
		* `g` to create a *GPT partition table*
		* `n` to add new partition
		* `w` to write changes to disk
1. Once the partition is made, format it. For example:
	* `mkfs.ext4 /dev/sdc1`
1. Mount via *UUID* as seen below

### Mount a folder as another drive:
1. edit `/etc/fstab`
	* `/path/to/source/folder	/mount/point	none	bind,nobootwait,_netdev 0 0`
	* this can be used to mount `/var/www` on a separate drive, yet retain existing paths
		* don't forget to copy the permissions of the original folder that gets moved to the new mount point

### Mount via UUID
1. get UUID
	* `sudo blkid /dev/sdxy`
1. enter into `/etc/fstab`
	* `UUID=[uuidnobrackets] /mount/point ext4 defaults `
