<!-- permalink: a6fe3a777cea529a24e0e738eb19c6e6 DO NOT DELETE OR EDIT THIS LINE -->
# Docker Reference

(no brackets in commands unless specified)


### Setup

* Install Docker
	* `curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh`
	* obviously, if you want to inspect the shell file before running it, you can modify the command and look it over

* Download an image
	* `docker pull [image-name]`

### Containers
* Create a container and run it in background
	* `docker run -d --rm -p 8080:80 --name [createANameHere] --network [networkName] [image-name] [commandToRun]`
	* `-d` means *detach* and will run it in the background
	* `--rm` will delete the container after it has stopped
	* `-p [containerPort]:[hostPort]` connects the port on the host the port on the container **NOTE** this can (and DOES in the case of ufw) override firewall settings! only use for services you want exposed on the host's network! (use `docker network` for internal communication between containers) 
	* `--network` and its followup argument is optional, but recommended for production (more on networks below)

* Create a container and use it interactively
	* `docker run -it --rm --name [createANameHere] [image-name] [commandToRun]`
		* for example `docker run -it --rm --name SwiftTest swift:5.7`

* List containers
	* `docker container ls -a`
	* `-a` lists all containers, not just those running currently

* Connect to existing, running container's main process
	* `docker container attach [containerName]`
	* **Note**: The attach command will display the output of the ENTRYPOINT/CMD process. This can appear as if the attach command is hung when in fact the process may simply not be interacting with the terminal at that time. [ref](https://docs.docker.com/engine/reference/commandline/attach/#extended-description)

* Run a new process in an existing, running container (best not to do in production)
	* `docker -exec -it [containerName] [command (like /bin/bash)]`

* Detach from a docker container
	* Hit `Ctrl-p` and then `Ctrl-q`
	* can be done without releasing `Ctrl` key

### Networks

* Create a network
	* `docker network create --driver bridge [newNetworkName]`
	* `--driver` is optional as `bridge` is the default value
		* options:
			* `bridge` - default - can communicate with others on same *docker network* as well as the internet
			* `overlay` - can communicate with other docker hosts - untested
	* containers can communicate with each other using container names on custom networks
		* alternatively, on the default network, you can only communicate with other containers via their ip
	* containers **CANNOT** communicate with containers on the same host UNLESS they share a network
	* containers created without specifying a network are automatically connected to the network named `bridge` (not to be confused with the driver named `bridge`)
	* containers can only be connected to one network at instantiation, but more can be added once created

* list networks
	* `docker network ls`

* connect existing container to a network
	* `docker network connect [networkName] [containerName]`

* inspect a network
	* `docker network inspect [networkName]`

### Dockerfile
used to create docker images

* a very basic *dockerfile* looks like this:

		FROM [upstreamImageName]
		MAINTAINER Your Name (email@address.com)
		RUN [commandToRunDuringImageSetup]
		COPY [local file or directory] [/path/to/a/conf/directory/in/image]
		ENTRYPOINT ["command" , "arg1", "arg2", "..."] #brackets actually used here
		CMD ["altPlaceForArg1", "altPlaceForArg2"] #brackets also here
		EXPOSE [port exposed to host]

	* example:

			FROM ubuntu:latest
			MAINTAINER Your Name (email@address.com)
			RUN apt update
			RUN apt install nginx
			COPY default.conf /etc/nginx/conf.d/
			ENTRYPOINT ["/usr/sbin/nginx" , "-g", "daemon-off;"] #brackets actually used here
			EXPOSE 80

* build this image (while in the same directory:
	* `docker build -t my-nginx-server:latest .`
	* `-t` means to tag the image

* run this image
	* `docker run -d -p 80:80 --name webserver my-nginx-server`
	* go to your server's ip in a browser to see the nginx default install landing page

### Compose?
deploys containers via yaml script

* docker compose used to be installed via a separate standalone executable, but now it's included in the default docker install. You can use it with the `docker compose` command
