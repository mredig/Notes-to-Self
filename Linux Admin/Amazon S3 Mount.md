# Amazon S3 Mount

This will allow you to mount S3 (both Amazon and third parties) buckets as local storage in Linux.

1. install *s3fs*
	* `apt install s3fs`
1. Create a credentials file
	1. in your home directory, create a file called *.password-s3fs* and place the access and secret keys inside:
		* `echo ACCESS_KEY:SECRET_KEY > ~/.passwd-s3fs`
	1. make sure this file is secured with no one else having access
		* `chmod 600 ~/.passwd-s3fs`
1. Create a mount point
	* `mkdir ~/s3Bucket`
1. Mount it (the `-o url=` option is only if you aren't using Amazon as your provider):
	* `s3fs [bucketNameNoBrackets] ~/s3Bucket -o passwd_file=~/.passwd-s3fs -o url=https://s3.wasabisys.com`
	* `s3fs [bucketNameNoBrackets] ~/s3Bucket -o url=https://s3.wasabisys.com`
