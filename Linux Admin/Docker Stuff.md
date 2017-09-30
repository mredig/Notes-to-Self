<!-- permalink: 9e9445e7de08ebc4e804416572bbf781 DO NOT DELETE OR EDIT THIS LINE -->
# Docker Stuff

* vocab
	* *image* - read only - it is just the source blob that a container is created from
	* *container* - the executing image that can be written to and used (but treat it as if it is ephemeral)

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
	* if you encounter `--link` your resource is **OLD** - go to a new tutorial
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


* Dockerfile
	* config for an image
	* can be done from scratch or based on another, existing image
	* can add files, create default volumes, ports, etc
	* private or public on Docker Hub

	* build it:
		* `docker bulid -t tag_name [build context path]`
		* `docker run -d --name app -v $(pwd):/var/www -p 8080:80 d4dapp`
		* `-f` specify a different filename for Dockerfile
		* `--no-cache`
		* `--pull` - always pull a new version

* Composer (php)
	* `docker run --rm -ti -v /home/mredig/.composer:/root/.composer -v $(pwd):/app -v /home/mredig/.ssh:/root/.ssh composer/composer install`

* Docker Compose
	* multi container orchestration
	* single config file holding all your container info
	* works with docker swarm

	* build yaml file from cd in daemon mode
		* `docker-compose up -d`


docker run --rm -v $(pwd):/opt -w /opt php:cli vendor/bin/phinx init


## production considerations
(these are notes from a conference - might be a bit rough)

1. codebase tracked in version control
	* repo tips
		* keep everything in repo
		* tag releases
		* never move tags
1. explicitly declare and isolate dependencies
	* commit both `composer.json` and `composer.lock` file
	* commit `Dockerfiles` to same repo as the codebase
1. Config
	* store config in environment
	* anything that is environment specific should move to the environment variables
	* makes it much easier to build and deploy code
	* code cares less what external services it is talking to
1. Backing services
	* everything is external
		* never talk to local sockets
		* don't make determination between locally hosted and third party
		* easier to switch environments
		* easier to scale up
1. Build, release, run
	* strictly separate steps
	* build installs all dependencies, compiles files, and generates *build artifact*
		* does NOT contain any deployment config
	* release step pushes *build artifact* into environment
		* runs db migrations, anything needed to happen before running
	* run steps runs the app fully in the environment
	* Tips:
		* *build artifacts* can be an image
		* builds should be completely reproducible
		* release always take a *build artifact*, never directly from the repo
		* tag all your builds
		* track all your releases
	* build step - start-small
		* build your application
			* run composer
			* run npm/bower
			* build js/css
		* use the compiled output to build.....
1. process
	* built into docker
		* one process per container
		* allows tools to scale just to what needs to be scaled
		* allows images to be swapped out as needed
1. Port binding
	* export services via port binding
		* built into docker
			* each container gets its own ip and exposes its own ports
			* process should already be talking over a network
			* can work with service locators that are port based
1. Concurrency
	* scale out via the process model
		* scale up just the container that is needed
		* app should not care how many instances of each service are running
1. Disposability
	* fast startup and quick shutdown
	* docker starts containers fairly quickly
	* applications should gracefully shut down, not just die
	* docker sends a SIGTERM when shutting down a container
1. Dev/prod parity
	* keep development, staging, and production as similar as possible
1. logs
	* treat logs as event streams
		* logging options built in to docker
			* JSON
			* fluentd
			* syslog
			* journald
			* gelf
			* splunk
			* aws
			* etwlogs
			* gcplogs
	* push logs remotely
		* when possible, push docker logs to a remote service
			* cannot use `docker logs` if doing anything other than json
		* allow logs to be viewed in a single place
1. admin process
	* run admin/management tasks as one off processes
