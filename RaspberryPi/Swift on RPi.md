# Swift on RPi3 Raspbian

1. Download from [this site](http://swift-arm.ddns.net/job/Swift-3.0-Pi3-ARM-Incremental/)
1. Update to stretch *gcc* [ref](https://github.com/doublethinkco/cpp-ethereum-cross/issues/79)
	1. `sudo nano /etc/apt/sources.list`
	1. Replace *jessie* with *stretch* in that file to point to the testing repository that has the gcc-5 package (or add new line with stretch)
	1. `sudo apt-get update`
	1. `sudo apt-get install gcc-5`
	1. `sudo apt-get upgrade`
	1. 






* random reference: [1](https://www.uraimo.com/2016/03/10/swift-3-available-on-armv6-raspberry-1-zero/) [2](http://saygoodnight.com/2016/05/08/building-swift-for-armv6.html) [3](http://blog.andrewmadsen.com/post/136137396480/swift-on-raspberry-pi) [4](http://dev.iachieved.it/iachievedit/swift-3-0-on-raspberry-pi-2-and-3/) [5](http://dev.iachieved.it/iachievedit/building-swift-3-0-on-a-raspberry-pi-3/)
