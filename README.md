# Docker
![Docker Logo](https://www.brianweet.com/assets/docker-blog-1/docker-logo.png)
## The Docker Lifecycle
* __Starting the Service in Linux__ -> `sudo service docker start`
* ___Create Container___ -> `docker create <imageName>`
  * The docker client will search locally the image or it will reach the Docker hub to grab the image
* ___Start container___ -> `docker start <id> <defaultCommand>`
  * The filesystem of the image gets copy to the container allongside the default command
  * Once running the container, the default command cant be overrided
  * If you want to execute other commands you will have to use the exec command `docker exec <containerId> <command>`
  * You can read and enter text into the container with the *-it* flags `docker exec -it <containerId> <command>` 
  * Many images have shells that you can run. To enter the filesystem with the shell use `docker run -it <containerName> sh `
> You can make create and start the container at once with `docker run <id> or  <ImageName> <defaultCommand>`

* Paused State
* ___Stop the Container___
  * You can either send a _SIGTERM_ signal with `docker stop <id>` to give it 10 seconds to gracefully shutdown
  * Or, you can send a _SIGKILL_ with `docker kill <containerId>` to shutdown inmediatly 
___  
## Creating your own Images
You can use other images by writting a **Dockerfile**

The docker Image can have:
1. A base Image using the commands `FROM <baseImage>` like ` FROM node:alpine`
2. Specifying the proccess the container will execute `RUN <command>` like `RUN npm install`
3. Defining the post-command with `CMD["string array"]` like `CMD ["npm","start"]`

To make a container from your own custom image you will run `docker build .` where the **.** is the context.

You can **copy** local files to your docker container with the `COPY` command like `COPY ./ ./` to copy the root directory to the container root directory
* If you want to copy anywhere else in the container you can use the `WORKDIR ` command like `WORKDIR '/app'`

You can also tag your instances with `docker build -t <yourName/nameOfContainer:version> .` so you dont have to run the container with the id.

If you want to anyways run the the container using the id you can just copy a couple of first alphanumeric characters and Docker will identify wich id is the correct container

A container will have by default the output ports closed to the outside world (*input ports are open by default*) to **map ports** you can use `docker run -p <localPortNumber>:<containerPortNumber> <imageName>` 

## Running multiple containers that commnicate with eachother
You can use the Docker cli to handle multiple containers and make a network between your containers but this is ~~pain in the ass~~. It is better to use a tool name **Docker Compose**

You will have to create a **docker-compose.yml**
In it you will enter

1. The version like `version: 3`
2. The services (the container) `services` like 
   1. `redis-server:`
      1. `image: redis`
3. You can set optional options like:
   |   Flag    | command|
   |-----------|--------|
   | `restart` | always |
   |  `build`    |   .    |
   | `ports`| "4001:8080"|

To create and run  `docker-compose up --`

To rebuild the containers when you change your source files `docker-compose up --build`

To kill the containers `docker-compose down`
___
## Docker useful commands

* `docker ps` -> Look the active containers

* `docker ps --all` Look the running containers and the ones that are stopped. 

* `docker images` -> Look to all the images you have downloaded
* `docker rmi <IMAGEID>` -> remove a docker image

* `docker inspect <repository>` -> Inspect a repository

* `docker rm <ContainerId>` -> Remove a Container

* `docker run -d <containerId>` -> Run withouts outputting the results

* `docker system prune` Remove all your images and erease the cache. 

* `docker logs <containerId>` -> Watch all the output the container has generated

* `docker image -q` -> Get the id of and image
## Terminology

**Alpine** : minimal

## Links
* [Docker Hub](https://hub.docker.com/)

* [Great Docker and Kubernetes Course](https://www.udemy.com/docker-and-kubernetes-the-complete-guide/)