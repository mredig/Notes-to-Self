<!-- permalink: 16d5905a76daf3851e4d3eed5bdb1fe4 DO NOT DELETE OR EDIT THIS LINE -->
# Creating SSH key files for passwordless login

###Client Machine
1. On client machine, run `ssh-keygen -t rsa -b 4096`
	* This is very secure
2. It'll ask you where to save it. By default it'll be a file named `id_rsa` stored in `~/.ssh` - Be sure that if you want a different file name, you type out the whole path of its destination.
3. You can add a password if you want, but I haven't experimented with how it implements this much.
4. After generation, it'll also have created a sister file called `id_rsa.pub`. This is your public key. Somehow get the contents of that file to the server.
	* `scp ~/.ssh/id_rsa.pub example_user@host_name_or_ip:~/authorized_keys` (and then move to the *.ssh* folder)

If you're managing more than one of these files, you need to be careful about overwriting the original *id_rsa* file. If you want to have different keys for each server, simply create the file *~/.ssh/config* and input the following contents (showing more than one entry in example):

* Nickname: *webpi*
* Hostname: *webpi.local*
* Username: *this_remote_user*

		Host webpi
		        HostName webpi.local
		        IdentityFile ~/.ssh/additional_id_rsa_file
		        User this_remote_user
				Port 22 #optional
		Host server2
				HostName server2.local
				IdentityFile ~/.ssh/other_additional_id_rsa_file
				User this_remote_user
				Port 22000 #required

From here on out you can just use

	ssh webpi

to connect with the presets above


###Server Machine
1. Copy the contents of the public key into `.ssh/authorized_keys`
	* authorized_keys is one line per key (the public key file should only have been one line, so that shouldn't be an issue)
1. Set permissions
	* `chmod -R 700 .ssh`

That's it!

You should now be able to do `ssh server.address` and be able to connect securely, without a password! The catch in this scenario is simply that the usernames must match. Otherwise you will need to `ssh server.address -l remoteUserName`. Additionally, if you named your identity file (or located it anywhere other than the default) you will need to specify the file with the -i argument. `ssh server.address -i /path/to/identity/file/like/id_rsa`
