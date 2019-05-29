---
title: Some Docker Images From Docker Hub
date: 2019-04-25
tags: docker hub images
---

## [woahbase/alpine-vue](https://hub.docker.com/r/woahbase/alpine-vue)

* Small image for Vue CLI built on Alpine Linux + NodeJS
* 50.1M/16 layers

```
Container for Alpine Linux + VueJS CLI
This image containerizes the command line client for VueJS along with its NPM dependencies.

Based on Alpine Linux from my alpine-nodejs image with the s6 init system overlayed in it.

The image is tagged respectively for the following architectures,

armhf
x86_64 ( retagged as the latest )
armhf builds have embedded binfmt_misc support and contain the qemu-user-static binary that allows for running it also inside an x64 environment that has it.

Get the Image
Pull the image for your architecture it's already available from Docker Hub.

# make pull
docker pull woahbase/alpine-vue:x86_64
Run
If you want to run images for other architectures, you will need to have binfmt support configured for your machine. multiarch, has made it easy for us containing that into a docker container.

# make regbinfmt
docker run --rm --privileged multiarch/qemu-user-static:register --reset
Without the above, you can still run the image that is made for your architecture, e.g for an x86_64 machine..

This images already has a user alpine configured to drop privileges to the passed PUID/PGID which is ideal if its used to run in non-root mode. That way you only need to specify the values at runtime and pass the -u alpine if need be. (run id in your terminal to see your own PUID/PGID values.)

Before you run..

Mount the project directory (where package.json is) at /home/alpine/project. Mounts PWD by default.

Vue runs under the user alpine.

Running make gets a shell.

# make
docker run --rm -it \
  --name docker_vue --hostname vue \
  -e PGID=1000 -e PUID=1000 \
  -c 256 -m 512m \
  -v $PWD:/home/alpine/project \
  -v /etc/localtime:/etc/localtime:ro \
  -v /etc/hosts:/etc/hosts:ro \
  -p 8080:8080 \
  --entrypoint /bin/bash \
  woahbase/alpine-vue:x86_64
The usual vue stuff. e.g list projects with

# make list
docker run --rm -it \
  --name docker_vue --hostname vue \
  -e PGID=1000 -e PUID=1000 \
  -c 256 -m 512m \
  -v $PWD:/home/alpine/project \
  -v /etc/localtime:/etc/localtime:ro \
  -v /etc/hosts:/etc/hosts:ro \
  -p 8080:8080 \
  woahbase/alpine-vue:x86_64 \
  list
initialize a project

# make init
docker run --rm -it \
  --name docker_vue --hostname vue \
  -e PGID=1000 -e PUID=1000 \
  -c 256 -m 512m \
  -v $PWD:/home/alpine/project \
  -v /etc/localtime:/etc/localtime:ro \
  -v /etc/hosts:/etc/hosts:ro \
  -p 8080:8080 \
  woahbase/alpine-vue:x86_64 \
  init
run the dev server,

# make dev
docker run --rm -it \
  --name docker_vue --hostname vue \
  -e PGID=1000 -e PUID=1000 \
  -c 256 -m 512m \
  -v $PWD:/home/alpine/project \
  -v /etc/localtime:/etc/localtime:ro \
  -v /etc/hosts:/etc/hosts:ro \
  -p 8080:8080 \
  --entrypoint npm \
  woahbase/alpine-vue:x86_64 \
  run dev
build the project with

# make prod
docker run --rm -it \
  --name docker_vue --hostname vue \
  -e PGID=1000 -e PUID=1000 \
  -c 256 -m 512m \
  -v $PWD:/home/alpine/project \
  -v /etc/localtime:/etc/localtime:ro \
  -v /etc/hosts:/etc/hosts:ro \
  -p 8080:8080 \
  --entrypoint npm \
  woahbase/alpine-vue:x86_64 \
  run build
Stop the container with a timeout, (defaults to 2 seconds)

# make stop
docker stop -t 2 docker_vue
Removes the container, (always better to stop it first and -f only when needed most)

# make rm
docker rm -f docker_vue
Restart the container with

# make restart
docker restart docker_vue
Shell access
Get a shell inside a already running container,

# make shell
docker exec -it docker_vue /bin/bash
set user or login as root,

# make rshell
docker exec -u root -it docker_vue /bin/bash
To check logs of a running container in real time

# make logs
docker logs -f docker_vue
Development
If you have the repository access, you can clone and build the image yourself for your own system, and can push after.

Setup
Before you clone the repo, you must have Git, GNU make, and Docker setup on the machine.

git clone https://github.com/woahbase/alpine-vue
cd alpine-vue
You can always skip installing make but you will have to type the whole docker commands then instead of using the sweet make targets.

Build
You need to have binfmt_misc configured in your system to be able to build images for other architectures.

Otherwise to locally build the image for your system. [ARCH defaults to x86_64, need to be explicit when building for other architectures.]

# make ARCH=x86_64 build
# sets up binfmt if not x86_64
docker build --rm --compress --force-rm \
  --no-cache=true --pull \
  -f ./Dockerfile_x86_64 \
  --build-arg ARCH=x86_64 \
  --build-arg DOCKERSRC=alpine-nodejs \
  --build-arg PGID=1000 \
  --build-arg PUID=1000 \
  --build-arg USERNAME=woahbase \
  -t woahbase/alpine-vue:x86_64 \
  .
To check if its working..

# make ARCH=x86_64 test
docker run --rm -it \
  --name docker_vue --hostname vue \
  -e PGID=1000 -e PUID=1000 \
  woahbase/alpine-vue:x86_64 \
  --version
And finally, if you have push access,

# make ARCH=x86_64 push
docker push woahbase/alpine-vue:x86_64
```

## [woahbase/alpine-nodejs](https://hub.docker.com/r/woahbase/alpine-nodejs)

* Alpine Linux + s6 + NodeJS + NPM
* 39.9M/11 layers

```
Container for Alpine Linux + S6 + NodeJS + NPM
This image serves as the base image for applications / services that require NodeJS and NPM to manage dependencies.

Based on Alpine Linux from my alpine-s6 image with the s6 init system overlayed in it.

The image is tagged respectively for the following architectures,

armhf
x86_64 ( retagged as the latest )
armhf builds have embedded binfmt_misc support and contain the qemu-user-static binary that allows for running it also inside an x64 environment that has it.

Get the Image
Pull the image for your architecture it's already available from Docker Hub.

# make pull
docker pull woahbase/alpine-nodejs:x86_64
Run
If you want to run images for other architectures, you will need to have binfmt support configured for your machine. multiarch, has made it easy for us containing that into a docker container.

# make regbinfmt
docker run --rm --privileged multiarch/qemu-user-static:register --reset
Without the above, you can still run the image that is made for your architecture, e.g for an x86_64 machine..

This images already has a user alpine configured to drop privileges to the passed PUID/PGID which is ideal if its used to run in non-root mode. That way you only need to specify the values at runtime and pass the -u alpine if need be. (run id in your terminal to see your own PUID/PGID values.)

Running make gets a shell.

# make
docker run --rm -it \
  --name docker_nodejs --hostname nodejs \
  -e PGID=1000 -e PUID=1000 \
  woahbase/alpine-nodejs:x86_64 \
  /bin/bash
Stop the container with a timeout, (defaults to 2 seconds)

# make stop
docker stop -t 2 docker_nodejs
Removes the container, (always better to stop it first and -f only when needed most)

# make rm
docker rm -f docker_nodejs
Restart the container with

# make restart
docker restart docker_nodejs
Shell access
Get a shell inside a already running container,

# make shell
docker exec -it docker_nodejs /bin/bash
set user or login as root,

# make rshell
docker exec -u root -it docker_nodejs /bin/bash
To check logs of a running container in real time

# make logs
docker logs -f docker_nodejs
Development
If you have the repository access, you can clone and build the image yourself for your own system, and can push after.

Setup
Before you clone the repo, you must have Git, GNU make, and Docker setup on the machine.

git clone https://github.com/woahbase/alpine-nodejs
cd alpine-nodejs
You can always skip installing make but you will have to type the whole docker commands then instead of using the sweet make targets.

Build
You need to have binfmt_misc configured in your system to be able to build images for other architectures.

Otherwise to locally build the image for your system. [ARCH defaults to x86_64, need to be explicit when building for other architectures.]

# make ARCH=x86_64 build
# sets up binfmt if not x86_64
docker build --rm --compress --force-rm \
  --no-cache=true --pull \
  -f ./Dockerfile_x86_64 \
  --build-arg ARCH=x86_64 \
  --build-arg DOCKERSRC=alpine-s6 \
  --build-arg PGID=1000 \
  --build-arg PUID=1000 \
  --build-arg USERNAME=woahbase \
  -t woahbase/alpine-nodejs:x86_64 \
  .
To check if its working..

# make ARCH=x86_64 test
docker run --rm -it \
  --name docker_nodejs --hostname nodejs \
  -e PGID=1000 -e PUID=1000 \
  woahbase/alpine-nodejs:x86_64 \
  sh -ec 'node --version; npm --version'
And finally, if you have push access,

# make ARCH=x86_64 push
docker push woahbase/alpine-nodejs:x86_64
```