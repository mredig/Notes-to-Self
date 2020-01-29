<!-- permalink: 8473eb1f3087ecd3c53e3d5bf0867d25 DO NOT DELETE OR EDIT THIS LINE -->
# Create Swapfile


Note that this all requires superuser priveleges.
1. Allocate filespace
	* `fallocate -l 2G /swapfile`
		* obviously replace `2G` with the actual amount you want to dedicate to swap
	* alternatively, `dd if=/dev/zero of=/swapfile bs=1024 count=1048576`
		* (1048576 = 1024 * 1024) - you can figure out how to get other sizes from here
1. Set permissions
	* `chmod 600 /swapfile`
1. set as swap
	* `mkswap /swapfile`
1. Enable swap
	* `swapon /swapfile`
1. Make permanent
	* add `/swapfile swap swap defaults 0 0` to `/etc/fstab`
1. confirm it's working (doesn't hurt to do this after a reboot to confirm it's persistent)
	* `swapon --show`

### Swappiness

1. Check the current swappiness value:
	* `cat /proc/sys/vm/swappiness`
1. Modify the swappiness level
	* edit the `/etc/sysctl.conf` file on line `vm.swappiness=**` and reboot
	* higher values allow more usage of swap, while lower values try harder to avoid using swap