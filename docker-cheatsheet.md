# Docker Cheatsheet

## Tutorial series

Get started with Docker: [https://docs.docker.com/engine/getstarted/](https://docs.docker.com/engine/getstarted/)

## Installation

### Linux

Install script provided by Docker:

```
curl -sSL https://get.docker.com/ | sh
```

Or see [Installation](https://docs.docker.com/engine/installation/linux/) instructions for your Linux distribution.


### Mac OS X

Download and install [Docker For Mac](https://docs.docker.com/docker-for-mac/)

### Create Docker VM with Docker Machine

You can use [Docker Machine](https://docs.docker.com/machine/) to:
- Install and run Docker on Mac or Windows
- Provision and manage multiple remote Docker hosts
- Provision Swarm clusters

A simple example to create a local Docker VM with VirtualBox: 

```
docker-machine create --driver=virtualbox default
docker-machine ls
eval "$(docker-machine env default)"
```

Then start up a container:

```
docker run alpine echo "hello-world"
```

That's it, you have a running Docker container.


## Container lifecycle

* Create a container: [`docker create imageName`](https://docs.docker.com/engine/reference/commandline/create).  
* Create and start a container in one operation: [`docker run imageName`](https://docs.docker.com/engine/reference/commandline/run)
  -  Remove the container after it stops `--rm`: `docker run  --rm alpine ls /usr/lib`
  -  Attach the container stdin/stdout to the current terminal use `-it`: `docker run -it ubuntu bash`
  -  To mount a directory on the host to a container add `-v` option, e.g. `docker run -v $HOSTDIR:$DOCKERDIR imageName` 
  -  To map a container port use `-p $HOSTPORT:$CONTAINERPORT`: `docker run -p 8080:80 nginx`
  -  To run the container in background use `-d` switch: `docker run -d -p 8080:80 nginx`
  -  Set container name: `docker run --name myContainerName imageName` 
  -  Example to run nginx web server to serve files from html directory on port 8080: 

```
    docker run -d -v $(pwd)/html:/usr/share/nginx/html -p 8080:80 --name myNginx nginx
    # access the webserver
    curl http://localhost:8080
``` 
* In some cases containers need [extended privileges](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities). Add privileges with the `--cap_add` switch, e.g. `docker run --cap-add SYS_ADMIN imageName`. The flag `--cap_drop` is used to remove privileges. 
* Rename a container: [`docker rename name newName`](https://docs.docker.com/engine/reference/commandline/rename/) 
* Delete a container: [`docker rm containerID`](https://docs.docker.com/engine/reference/commandline/rm)
  - Delete all unused containers: `docker ps -q -a | xargs docker rm`
  - Remove the volumes associated with a container: `docker rm -v containerName`
 
* Update container resource limits:
[`docker update --cpu-shares 512 -m 300M`](https://docs.docker.com/engine/reference/commandline/update/)  
* List running containers: [`docker ps`](https://docs.docker.com/engine/reference/commandline/ps/)
* List all containers: [`docker ps -a`](https://docs.docker.com/engine/reference/commandline/ps/)
* List all container IDs: [`docker ps -q -a`](https://docs.docker.com/engine/reference/commandline/ps/)

## Starting and stopping containers

* Start a container:
[`docker start containerName`](https://docs.docker.com/engine/reference/commandline/start) * [`docker stop`](https://docs.docker.com/engine/reference/commandline/stop) 
* Restart a container: [`docker restart containerName`](https://docs.docker.com/engine/reference/commandline/restart)
* Pause a container ("freeze"): [`docker pause containerName`](https://docs.docker.com/engine/reference/commandline/pause/)
* Unpause a container: [`docker unpause containerName `](https://docs.docker.com/engine/reference/commandline/unpause/) 
* Stop and wait for termination: [`docker wait containerName`](https://docs.docker.com/engine/reference/commandline/wait) 
* Kill a container (sends SIGKILL): [`docker kill containerName`](https://docs.docker.com/engine/reference/commandline/kill) 

## Executing commands in containers and apply changes

* Execute a command in a container: [`docker exec -it containerName command`](https://docs.docker.com/engine/reference/commandline/exec) 
* Copy files or folders between a container and the local filesystem: [`docker cp containerName:path localFile`](https://docs.docker.com/engine/reference/commandline/cp) or `docker cp localPath containerName:path`
* Apply changes in container file systems: [`docker commit containerName`](https://docs.docker.com/engine/reference/commandline/commit)


## Logging and monitoring

Logging on Docker could be challenging - check [Top 10 Docker Logging Gotchas](https://sematext.com/blog/top-10-docker-logging-gotchas/).

* Show container logs: [`docker logs containerName`](https://docs.docker.com/engine/reference/commandline/logs)
* Show only new logs: [`docker logs -f containerName`](https://docs.docker.com/engine/reference/commandline/logs)
* Show CPU and memory usage: [`docker stats`](https://docs.docker.com/engine/reference/commandline/stats)
* Show CPU and memory usage for specific containers: [`docker stats containerName1 containerName2`](https://docs.docker.com/engine/reference/commandline/stats)
* Show running processes in a container: [`docker top containerName`](https://docs.docker.com/engine/reference/commandline/top) 
* Show Docker events: [`docker events`](https://docs.docker.com/engine/reference/commandline/events) 
* Show storage usage: [`docker system df`](https://docs.docker.com/engine/reference/commandline/system_df) 
* To run a container with a custom [logging driver](https://docs.docker.com/engine/admin/logging/overview/) (i.e., to syslog), use: 
```
docker run -–log-driver syslog –-log-opt syslog-address=udp://syslog-server:514 \
alpine echo hello world
```
* Use [Logagent](https://sematext.com/logagent/) for log collection and [Sematext Agent](https://www.sematext.com/docker) for metrics and event monitoring. Create Docker Monitoring App & Logs App in [Sematext Cloud](https://sematext.com/cloud) to get required tokens and use them instead the placeholders `YourContainerToken`, `YourInfraToken` and `YourLogsToken` in commands below. Start collecting all container metrics, host metrics and Docker events:

```
docker run -d  --restart always --privileged -P --name st-agent \
-v /sys/kernel/debug:/sys/kernel/debug \
-v /var/run/:/var/run/ \
-v /proc:/host/proc:ro \
-v /etc:/host/etc:ro \
-v /sys:/host/sys:ro \
-v /usr/lib:/host/usr/lib:ro \
-e CONTAINER_TOKEN=YourContainerToken \
-e INFRA_TOKEN=YourInfraToken \
-e JOURNAL_DIR=/var/run/st-agent \
-e LOGGING_WRITE_EVENTS=false \
-e LOGGING_REQUEST_TRACKING=false \
-e LOGGING_LEVEL=info \
-e NODE_NAME=`hostname` \
-e CONTAINER_SKIP_BY_IMAGE=sematext \
sematext/agent:latest
```

Collect all container logs:

```
docker run -d --name st-logagent \
-e LOGS_TOKEN=YourLogsToken \
-v /var/run/docker.sock:/var/run/docker.sock \
sematext/logagent
```

The commands above will collect all container metrics, host metrics, Docker events, and container logs. 


## Exploring Docker information

* Show Docker info: [`docker info`](https://docs.docker.com/engine/reference/commandline/info)
* List all containers: [`docker ps -a`](https://docs.docker.com/engine/reference/commandline/ps) 
* List all images: [`docker image ls`](https://docs.docker.com/engine/reference/commandline/image_ls) 
* Show all container details: [`docker inspect containerName`](https://docs.docker.com/engine/reference/commandline/inspect) 
* Show changes in the container's files:[`docker diff containerName`](https://docs.docker.com/engine/reference/commandline/diff) 


## Manage Docker images

* List all images: [`docker images`](https://docs.docker.com/engine/reference/commandline/images) 
* Search in registry for an image:
[`docker search searchTerm`](https://docs.docker.com/engine/reference/commandline/search) 
* Pull image from a registry: [`docker pull imageName`](https://docs.docker.com/engine/reference/commandline/pull) pulls an image from registry to local machine
* Create image from Dockerfile: [`docker build`](https://docs.docker.com/engine/reference/commandline/build)
* Remove image: [`docker rmi imageName`](https://docs.docker.com/engine/reference/commandline/rmi) 
* Export container into tgz file: [`docker export myContainerName -o myContainerName `](https://docs.docker.com/engine/reference/commandline/export) 
* Create an image from a tgz file:[`docker import file`](https://docs.docker.com/engine/reference/commandline/import) 

## Docker networks

* List existing networks: [`docker network ls`](https://docs.docker.com/engine/reference/commandline/network_ls/)
* Create a network: [`docker network create netName`](https://docs.docker.com/engine/reference/commandline/network_create/)
* Remove network: [`docker network rm netName`](https://docs.docker.com/engine/reference/commandline/network_rm/)
* Show network details: [`docker network inspect`](https://docs.docker.com/engine/reference/commandline/network_inspect/)
* Connect container to a network: [`docker network connect networkName containerName`](https://docs.docker.com/engine/reference/commandline/network_connect/)
* Disconnect network from container: [`docker network disconnect networkName containerName`](https://docs.docker.com/engine/reference/commandline/network_disconnect/)

## Data cleanup 

Data management commands:

* Remove unused resources: [`docker system prune`](https://docs.docker.com/engine/reference/commandline/system_prune/)
* Remove unused volumes: [`docker volume prune`](https://docs.docker.com/engine/reference/commandline/volume_prune/)
* Remove unused networks: [`docker network prune`](https://docs.docker.com/engine/reference/commandline/network_prune/)
* Remove unused containers: [`docker container prune`](https://docs.docker.com/engine/reference/commandline/network_prune/)
* Remove unused images: [`docker image prune`](https://docs.docker.com/engine/reference/commandline/network_prune/)
