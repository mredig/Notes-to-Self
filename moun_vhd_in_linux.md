# Mounting VHD on Linux

1. Add to /etc/apt/sources.list `deb http://download.virtualbox.org/virtualbox/debian xenial contrib`
	* According to your distribution, replace 'xenial' by 'vivid', 'utopic', 'trusty', 'raring', 'quantal', 'precise', 'lucid', 'jessie', 'wheezy', or 'squeeze'. 
2. run `sudo apt-get install virtualbox-5.0`
3. Download [this](http://launchpadlibrarian.net/124207401/virtualbox-fuse_4.1.22-dfsg-0ubuntu2_amd64.deb) if that doesn't work, I got it from this [page](https://launchpad.net/ubuntu/raring/amd64/virtualbox-fuse/4.1.22-dfsg-0ubuntu2) which I got to from [THIS PAGE](https://launchpad.net/ubuntu/raring/amd64/virtualbox-fuse/4.1.22-dfsg-0ubuntu2)
4. run `dpkg -i --force-depends /path/to/deb/file/downloaded/a/step/ago.deb`
5. these commands should get you there from here on:

* `sudo mkdir /mnt/vhd-disk/`
* `sudo vdfuse -f disk.vhd /mnt/vhd-disk/`
* `sudo mkdir /mnt/partition*/`
* `sudo mount /mnt/vhd-disk/Partition* /mnt/partition*`



##### Sources
http://key-value.blogspot.com/2013/06/mounting-vhd-image-file-in-linux.html
https://www.virtualbox.org/wiki/Linux_Downloads
https://launchpad.net/ubuntu/raring/amd64/virtualbox-fuse/4.1.22-dfsg-0ubuntu2
http://askubuntu.com/a/296017
