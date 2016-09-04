# Mount HFS plus on Linux

1. run updates
	* `sudo apt-get update`
	* `sudo apt-get upgrade`
1. Install client software
	* `sudo apt-get install hfsprogs`
1. Run one time command or add to *fstab*

### One time:

	sudo mount -t hfsplus -o force,rw /dev/sdXY /media/mntpoint


### **OR** add the following line to *fstab*

	/dev/sdXY   /media/mntpoint   hfsplus   force,rw


##### To repair an HFSplus drive:

	sudo fsck.hfsplus -f /dev/sdXY
