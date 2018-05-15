<!-- permalink: b1828aec0770c1a3a932443881d2d101 DO NOT DELETE OR EDIT THIS LINE -->
# KVM Disk Image Management


### Convert Disk Image Formats
1. With qemu installed, this works. In this example, converting from a *VDI VirtualBox* format to *Qcow2*. Note that that is -O (capital O) not -0 (zero)
	* `qemu-img convert -f vdi -O qcow2 ubuntu.vdi ubuntu.qcow2`


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
1. `virt-sparsify bloatedDiskImage.ext outputShrunkDiskImage.ext`
	* this appears to support `qcow2`, `vdi`, and `raw` (`img` I think?)
	* Conjecture - I think if you have a `qcow2` image you can use `--in-place` to avoid having to create a second image
	* [more info](http://libguestfs.org/virt-sparsify.1.html)
	* Alternatives
		* [1](https://serverfault.com/questions/432119/is-there-any-way-to-shrink-qcow2-image-without-converting-it-raw) look into virt-sparsify
		* [2](https://pve.proxmox.com/wiki/Shrink_Qcow2_Disk_Files#Shrink_the_Disk_File) - less efficient, but more stable?
		* [3](https://www.jamescoyle.net/how-to/323-reclaim-disk-space-from-a-sparse-image-file-qcow2-vmdk) - alt zeroing method
1. Be sure to test the resulting image before deleting the original
