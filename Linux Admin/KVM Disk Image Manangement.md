# KVM Disk Image Management



### Mount Disk Image in Linux
This is might be specific to qcow2 image files.

***DO NOT*** mount the disk image in read/write mode while the VM is running!

1. Install *libguestfs-tools*
	* `apt install libguestfs-tools`
1. Create a mount point:
	* `mkdir /mnt/guestIMG`
1. Mount it (replace device with anything to get a list of what devices are available):
	* `guestmount -a /path/to/qcow2/image -m <device> /mnt/guestIMG`
	* note that this does NOT require super user permissions if your user has full access to the mount point and image
	* use `guestmount -a /path/to/qcow2/image -m <device> --ro /mnt/guestIMG` to make it read only (which would allow you to mount while the VM is running)
1. Unmount it when finished:
	* `guestmount /mnt/guestIMG`
1. [resource](http://ask.xmodulo.com/mount-qcow2-disk-image-linux.html)


### Resize Qcow2 Disk Image
* TBD

### Shrink Qcow2 Disk Image
* TBD
