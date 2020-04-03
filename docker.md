# Docker

Docker is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels.

## Key

Command | Explanation
------- | -----------
`docker` | Reference the Docker client.
`exec` | Run another command.
`-it` | Allow us to provide input to the container. Combination of `-i` (attach to standard in) and `-t` (attach to standard out, nicely displays output).
`<container id>` | ID of the container.
`<command>` | Command to execute.
`-a` | Display all results. Attach this option to the container.

## Run Containers

### docker run

Command | Functionality | Output
------- | ------------- | ------
`docker run <image>` | Start a new container from an image.<br>`docker run` = `docker create` + `docker start` | `docker run nodejs`
`docker run -d <image>`| Start a new container from an image in a detached state. You can continue to use the CLI without seeing its immediate output. | `docker run -d nginx`
`docker run --name <container name> <image>` | Assign the container a name. | `docker run --name webapp nginx`
`docker run -p <host port>:<container port> <image>` | Map the container's ports. | `docker run -p 8080:80 nginx`
`docker run -P <image>` | Map all ports. | `docker run -P nginx`

### docker create

Command | Functionality | Output
------- | ------------- | ------
`docker create <image name>` | Creates a container from an image. | `docker create hello-world` <br><br>`Unable to find image 'hello-world:latest' locally` <br>`latest: Pulling from library/hello-world` <br>`1b930d010525: Pull complete` <br>`Digest: sha256:f9dfddf63636d84ef479d645ab5885156ae030f611a56f3a7ac7f2fdd86d7e4e` <br>`Status: Downloaded newer image for hello-world:latest` <br>`99686fc169930ed8edf67404fe8e11d289f7cc0efb444373182cd76f9e16932c`

### docker start

Command | Functionality | Output
------- | ------------- | ------
`docker start -a <id>` | Start a container. | `docker start -a 7fb44b5f5e7a7fcd1320d7c01de4e32479679d594ce97416ae6d70d3810a421a`

## Manage Containers

### docker ps

Command | Functionality | Output
------- | ------------- | ------
`docker ps` | List containers. | See table below.
`docker ps --all` or `docker ps -a` | List all containers, even if they've been stopped or exited. | See table below.

```
CONTAINER ID   IMAGE                    COMMAND                  CREATED      STATUS                PORTS                  NAMES
a2506c9c4550   httpd                    "/usr/sbin/init"         4 days ago   Up 4 days             0.0.0.0:8000->80/tcp   httpd
b7ca26bf433b   mysql/mysql-server:5.5   "/entrypoint.sh mysq…"   4 days ago   Up 4 days (healthy)   3306/tcp               cw-mysql
```

### docker logs

Command | Functionality | Output
------- | ------------- | ------
`docker logs <container id>` | Get logs from a container. | `docker logs e19f6f828ddc9254752388a474e50635db3cf4885cd7c3aa8d414d8ccd104ee6`
`docker exec -it` | Execute an additional command in a container. |
`docker images` | Display a list of all available images that have been downloaded.
`docker pull <container id>` | Download the container immediately without checking if it exists locally first. | `docker pull nginx`

## Clean Up

### Clean All

Command | Functionality
------- | -------------
`docker system prune` | Cleans up dangling images, containers, volumes, and networks (ie, not associated with a container).
`docker system prune -a` | Additionally remove any stopped containers and all unused images (not just dangling images).

### Clean Containers

Command | Functionality
------- | -------------
`docker stop <container id>` | Stop a container. If it doesn't shut down in 10 seconds it will automatically kill the container.
`docker kill <container id>` | Kill a container. |
`docker rm <container id>` | Removes a container. | `docker rm silly_sammet`
`docker container prune` | Delete stopped containers.

### Clean Images

Command | Functionality
------- | -------------
`docker rmi <image>` | Remove the image permanently. | `docker rmi nginx`
`docker image prune -a` | Delete all the images.

## Images vs. Container

An **image** is a package or template, similar to a VM template. It is used to create 1 or more containers.

**Containers** are running instances of images that are isolated and have their own environments and processes.

## To Categorize

`docker exec -it 0d2ccab14d7d redis-cli`

`docker exec -it 0d2ccab14d7d sh`

`docker exec <container> <command>` | Execute a command within the image. | `docker exec silly_sammet cat /etc/hosts`

Get shell.

`docker run -it busybox sh`

Writing a dockerfile is similar to being given a computer with no OS and being told to install Chrome.

Tag an image
`docker build -t mmaether/redis:latest .`

`copy ./ ./`
Command, path to folder to copy from on *your machine* relative to build context, Place to copy stuff to inside *the container*.

`docker run -p 8080:8080 <image id>`
`docker run -p 8080:8080 mmaether/simpleweb`
Route incoming requests to this port on local host to... this port inside the container.

## Port Mapping

![Docker port mapping](images/docker-port-mapping.jpg)

![Docker persist data](images/docker-persist-data.jpg)