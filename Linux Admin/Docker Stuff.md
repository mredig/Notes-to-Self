<!-- permalink: 9e9445e7de08ebc4e804416572bbf781 DO NOT DELETE OR EDIT THIS LINE -->
# Docker Stuff

* vocab
	* *image* is read only - it is just the source blob that a container is created from
	* *container* is the executing image that can be written to and used (but treat it as if it is ephemeral)

* Run Centos prompt
	* `docker run --rm -ti centos /bin/bash`
* Run nginx in background
	* `docker run -d --name=web1 -p 8080:80 nginx`
* run additional process in existing container (do NOT use in production)
	* `docker exec -ti web1 bash`


* Volumes
	* mount home tmp dir as html folder inside the container (dev only)
		* `docker run -v /home/[username]/tmp:/usr/share/nginx/html -d --name=web1 -p 8080:80 nginx`
	* named volumes
		* create space that becomes persistent
		* mounted anywhere inside images

	* Create a named volume *webdata*
		* `docker volume create webdata`
			* creates a locally hosted folder by default - can be used with external storage (better)
		* `docker run -v webdata:/usr/share/nginx/html -d --name=web1 -p 8080:80 nginx`

* Networking
	* `--link` is OLD - go to a new tutorial

	* create a new docker network
		* `docker network create sampleapp`
	* use the previously created network and provide a "dns" name
		* `docker run --network sampleapp --network-alias web -d --name=web1 -p 8080:80 nginx`
	* specialized image to ping the new container via "dns"
		* `docker run -ti --network sampleapp alpine ping web`


* MISC
	* returns JSON query string with data about container
		* `docker inspect [options] CONTAINER_NAME`
	* removes an image if not being used
		* `docker rmi IMAGE`
	* view logs from a docker container
		* `docker logs --tail 20 CONTAINER_NAME`
