# Swift On Linux

(specifically Ubuntu 18.04)

1. install the following: 
	* `clang libcurl3 libpython2.7 libpython2.7-dev git mosh curl`
	* (`apt install -y`)
1. download swift:
	* [`https://swift.org/builds/swift-4.2.1-release/ubuntu1804/swift-4.2.1-RELEASE/swift-4.2.1-RELEASE-ubuntu18.04.tar.gz`](https://swift.org/builds/swift-4.2.1-release/ubuntu1804/swift-4.2.1-RELEASE/swift-4.2.1-RELEASE-ubuntu18.04.tar.gz)
1. install swift:
	1. `echo "export PATH=/usr/share/swift/usr/bin:$PATH" >> ~/.bashrc`
	1. `source  ~/.bashrc`
1. verify it's installed:
	* `swift --version`
