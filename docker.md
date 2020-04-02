# Docker

Docker is a set of platform as a service products that uses OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels.

`docker ps`

```
CONTAINER ID   IMAGE                    COMMAND                  CREATED      STATUS                PORTS                  NAMES
a2506c9c4550   httpd                    "/usr/sbin/init"         4 days ago   Up 4 days             0.0.0.0:8000->80/tcp   httpd
b7ca26bf433b   mysql/mysql-server:5.5   "/entrypoint.sh mysq…"   4 days ago   Up 4 days (healthy)   3306/tcp               cw-mysql
```

Command | Functionality | Output
------- | ------------- | ------
`docker ps` | List containers. | See Docker table above.
`docker ps --all` | List all containers that have ever been created. | See Docker table above.
`docker run` | Run a command in a new container. <br>`docker run` = `docker create` + `docker start` | `docker run mongodb` <br>`docker run redis` <br>`docker run nodejs`
`docker create <image name>` | Create a new container. | `docker create hello-world` <br><br>`Unable to find image 'hello-world:latest' locally` <br>`latest: Pulling from library/hello-world` <br>`1b930d010525: Pull complete` <br>`Digest: sha256:f9dfddf63636d84ef479d645ab5885156ae030f611a56f3a7ac7f2fdd86d7e4e` <br>`Status: Downloaded newer image for hello-world:latest` <br>`99686fc169930ed8edf67404fe8e11d289f7cc0efb444373182cd76f9e16932c`
`docker system prune` | Delete all containers, all networks not used by at least one container, dangling images, and build cache.
`docker logs <container id>` | Get logs from a container. | `docker logs e19f6f828ddc9254752388a474e50635db3cf4885cd7c3aa8d414d8ccd104ee6`
`docker exec -it` | Execute an additional command in a container. | 
`docker kill <container id>` | Kill a container. | 
`docker stop <container id>` | Stop a container. If it doesn't shut down in 10 seconds it will automatically kill the container. |
`docker start -a <id>` | Start a container. | `docker start -a 7fb44b5f5e7a7fcd1320d7c01de4e32479679d594ce97416ae6d70d3810a421a`

`-a` = Attach to the container.


Command | Explanation
------- | -----------
docker | Reference the Docker client.
exec | Run another command.
-it | Allow us to provide input to the container. Combination of `-i` (attach to standard in) and `-t` (attach to standard out, nicely displays output).
`<container id>` | ID of the container.
`<command>` | Command to execute.

`docker exec -it 0d2ccab14d7d redis-cli`

`docker exec -it 0d2ccab14d7d sh`

Get shell.

`docker run -it busybox sh`

Writing a dockerfile is similar to being given a computer with no OS and being told to install Chrome.

Tag an image
`docker build -t mmaether/redis:latest .`

Image vs. Container

Image | Container
----- | ---------
An image is a package or template, similar to a VM template. It is used to create 1 or more containers. | Containers are running instances of images that are isolated and have their own environments and processes.

`copy ./ ./`
Command, path to folder to copy from on *your machine* relative to build context, Place to copy stuff to inside *the container*.

`docker run -p 8080:8080 <image id>`
`docker run -p 8080:8080 mmaether/simpleweb`
Route incoming requests to this port on local host to... this port inside the container.
