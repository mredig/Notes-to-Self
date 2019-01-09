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
* Create a container and run it
	* `docker run -d --rm --name [createANameHere] --network [networkName] [image-name] [commandToRun]`
	* `-d` means *detach* and will run it in the background
	* `--rm` will delete the container after it has stopped
	* `--network` and its followup argument is optional, but recommende for production (more on networks below)

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
	* containers created without specifying a network are automatically connected to the network named `bridge` (not to be confused with the driver named `bridge`)
	* containers can only be connected to one network at instantiation, but more can be added once created

* list networks
	* `docker network ls`

* connect existing container to a network
	* `docker network connect [networkName] [containerName]`

* inspect a network
	* `docker network inspect [networkName]`

### Dockerfile
* used to create docker images
tbd

### Compose?
deploys containers via scripting i think?
tbd