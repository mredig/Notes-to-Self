<!-- permalink: 7ee411b43039c7b0439a9a0d1609975f DO NOT DELETE OR EDIT THIS LINE -->
# Swift On Linux

(specifically Ubuntu 18.04)

1. install the following: 
	* `clang libcurl3 libpython2.7 libpython2.7-dev git mosh curl`
	* (`apt install -y`)
1. download swift:
	* [`https://swift.org/builds/swift-5.1.4-release/ubuntu1804/swift-5.1.4-RELEASE/swift-5.1.4-RELEASE-ubuntu18.04.tar.gz`](https://swift.org/builds/swift-5.1.4-release/ubuntu1804/swift-5.1.4-RELEASE/swift-5.1.4-RELEASE-ubuntu18.04.tar.gz)
1. install swift:
	1. `tar -xvf swift-file.tar.gz`
	1. `sudo mv [unarchivedFolder] /usr/share/swift`
	1. `echo "export PATH=/usr/share/swift/usr/bin:$PATH" >> ~/.bashrc`
	1. `source  ~/.bashrc`
1. verify it's installed:
	* `swift --version`
