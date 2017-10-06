<!-- permalink: 2de12fff530d90a0545765c8ed41990c DO NOT DELETE OR EDIT THIS LINE -->
# Hyper-V Terminal Window Size

I have a few instances of Debian in a Hyper-V environment with small monitors. It's a real pain when the Debain command line prompt is larger than the monitor of the host system. This is how to fix that:

1. `nano /etc/default/grub`
1. Find the line `GRUB_CMDLINE_LINUX_DEFAULT="quiet"`
1. edit it to look like:
	* `GRUB_CMDLINE_LINUX_DEFAULT="quiet video=hyperv_fb:1024x768"`
		* you can change `1024x768` to any other resolution
1. save and exit
1. `update-grub`
1. reboot
