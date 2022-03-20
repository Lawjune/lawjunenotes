# Notes from CodeWithMosh

## Introduction to Docker

### What is Docker

*A platform for building, running and shipping applications.*

**Why this software isn't working on my machine?
* One or more files missing
* Software version mismatch
* Different configuration settings
**

**Consistently**
*build, run and ship applications*

### Virtual Machines vs Containers

**VIRTUAL MACHINE**
*An abstraction of a machine (physical hardware)*
->*PROBLEMS*
* Each VM needs a full-blown OS
* Slow to start
* Resource intensive

**CONTAINER**
*An isolated environment for running an application*
* Allow running multiple applications in isolation
* Are lightweght
* Use OS of the host
* Start quickly
* Need less hardware resource

### Docker Architecture

**CLIENT -> RESTFUL API-> DOCKER ENGINE**

*All of the applications in the docker share the kernel of OS.*
*A kernel manages applications and hardware resource.*

* Windows -> Windows + Linux
* Linux -> Linux 
* Mac -> Linux VM

### Installing Docker

```sh
docker version
```

### Development Workflow

*Use `Dockerfile` to pack apps into the image.*

**IMAGE**
* A cut-down OS
* A runtime environment (eg Node)
* Application files
* Third-porty libraries
* Environment variables

**DOCKER**
*[DEV] -> [REGISTRY] -> [TEST/PROD]*

**DOCKER**
*[DEV] -> [STAGE] -> [TEST/PROD]*

### Docker in Action

*The latest version of Docker uses the new build tool called the BuildKit which displays a more compact and colorized output. In the previous versions, we could optionally enable the BuildKit by setting an environment variable. In the latest version, the BuildKit is enabled by default.*

**INSTRUCTIONS**
* Start with an OS
* Install Node
* Copy app files
* Run node app.js

```sh
docker build -t hello-docker .
```

```sh
docker image ls
`=>
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
hello-docker   latest    52e9740d7daa   21 seconds ago   110MB
```

```sh
docker run hello-docker
`=>
Hello Docker!
```

## Buiding Images

### Introduction

**Having a solid understanding of Docker Images is crucial!**

* Creating Docker files 
* Versioning images
* Sharing images
* Saving and loading images
* Reducing the image size 

### Images and Containers

**IMAGE
* A cut-down OS 
* Third-party libraries
* Application files
* Environment variables
**

**CONTAINER
* Provides an isolated environment 
* Can be stopped & restarted
* Is just a process!
**

### Sample Web Application

*Use `react-app`*

### Dockerfile Instructions

**A Dockerfile contains instructions for building an image.**

**DOCKERFILE
* FROM
* WORKDIR 
* COPY
* ADD
* RUN
* ENV
* EXPOSE
* USER
* CMD
* ENTRYPOINT
**

### Choosing the Right Base Image


```Dockerfile
FROM node:lts-alpine3.14
```

```sh
docker build -t react-app .
```

```sh
docker image ls
`=>
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
hello-docker   latest    52e9740d7daa   23 hours ago   110MB
ubuntu         latest    ba6acccedd29   3 days ago     72.8MB
react-app      latest    735daedabb47   6 days ago     118MB
```

```sh
docker run -it react-app
```
->*Running the node only*
->*Failed to run `docker run -it react-app bash` because alpine doesn't have `bash`.*

```sh
docker run -it react-app sh
```

### Copying Files and Directories

```Dockerfile
FROM node:lts-alpine3.14
WORKDIR /app
COPY . .
```

```sh
docker build -t react-app .
```

```sh
docker run -it react-app sh
```

```sh
/app # ls
`=>
Dockerfile         node_modules       package.json       src
README.md          package-lock.json  public             yarn.lock
```

### Excluding Files and Directories

*Create `.dockerignore` file*

```sh
echo "node_modules/" >> .dockerignore
```

### Running Commands

```Dockerfile
FROM node:lts-alpine3.14
WORKDIR /app
COPY . .
RUN npm install
```

### Setting Environment Variables

```Dockerfile
FROM node:lts-alpine3.14
WORKDIR /app
COPY . .
RUN npm install
ENV API_URL=http://api.appspot.com/
```

*Check the environment variable in the new built image running in the container.*

```sh
printenv API_URL
echo $API_URL
```

### Exposing Ports

```Dockerfile
FROM node:lts-alpine3.14
WORKDIR /app
COPY . .
RUN npm install
ENV API_URL=http://api.appspot.com/
EXPOSE 3000 
```

### Setting the User

```sh
docker run -it alpine
```

=>*Access into `alpine` container*

```sh
adduser
`=>
BusyBox v1.33.1 () multi-call binary.

Usage: adduser [OPTIONS] USER [GROUP]

Create new user, or add USER to GROUP

	-h DIR		Home directory
	-g GECOS	GECOS field
	-s SHELL	Login shell
	-G GRP		Group
	-S		Create a system user
	-D		Don't assign a password
	-H		Don't create home directory
	-u UID		User id
	-k SKEL		Skeleton directory (/etc/skel)
```

```sh
addgroup app
adduser -S -G app app
groups app
`=>
app
```

```sh
addgroup lawjune && adduser -S -G lawjune lawjune
groups lawjune
`=>
lawjune
```

### Defining Entrypoints

```Dockerfile
FROM node:lts-alpine3.14
RUN addgroup app && adduser -S -G app app
USER app
WORKDIR /app
COPY . .
RUN npm install
ENV API_URL=http://api.appspot.com/
EXPOSE 3000 
```

```sh
docker run react-app npm start
```

**Or to add the CMD in Dockerfile**

```Dockerfile
FROM node:lts-alpine3.14
RUN addgroup app && adduser -S -G app app
USER app
WORKDIR /app
COPY . .
RUN npm install
ENV API_URL=http://api.appspot.com/
EXPOSE 3000 
CMD npm start
```

*`RUN` is the build-time instruction for building the image.*
*`CMD` is the run-time instruction executing in the container.*

```sh
# Shell form
CMD npm start

# Exec form
CMD ["npm", "start"]
```

### Speeding Up Builds

```Dockerfile
FROM node:lts-alpine3.14
RUN addgroup app && adduser -S -G app app
USER app
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
ENV API_URL=http://api.appspot.com/
EXPOSE 3000 
CMD npm start
```

***Organize your Dockerfile
Stable instructions -> Changing instructions***


### Removing Images

```sh
docker container prune
docker image prune
```

```sh
docker images
`=>
REPOSITORY     TAG       IMAGE ID       CREATED         SIZE
react-app      latest    446feb548e5a   2 minutes ago   299MB
hello-docker   latest    52e9740d7daa   24 hours ago    110MB
ubuntu         latest    ba6acccedd29   3 days ago      72.8MB
alpine         latest    14119a10abf4   7 weeks ago     5.6MB
```

```sh
docker image rm hello-docker
```

### Tagging Images

```sh
docker build -t react-app:buster .
docker images          
`=>           
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
react-app    buster    446feb548e5a   7 minutes ago   299MB
react-app    latest    446feb548e5a   7 minutes ago   299MB
ubuntu       latest    ba6acccedd29   3 days ago      72.8MB
alpine       latest    14119a10abf4   7 weeks ago     5.6MB
```

```sh
docker image remove react-app:buster
`=>
Untagged: react-app:buster
```
```sh
docker images
`=>
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
react-app    latest    446feb548e5a   9 minutes ago   299MB
ubuntu       latest    ba6acccedd29   3 days ago      72.8MB
alpine       latest    14119a10abf4   7 weeks ago     5.6MB
```

```sh
docker image tag react-app:latest react-app:1
react-app % docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
react-app    1         446feb548e5a   10 minutes ago   299MB
react-app    latest    446feb548e5a   10 minutes ago   299MB
ubuntu       latest    ba6acccedd29   3 days ago       72.8MB
alpine       latest    14119a10abf4   7 weeks ago      5.6MB
```

*Modify the app and re-build.*

```sh
docker build -t react-app:2 .
docker images
`=>
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
react-app    2         d02f199fb61c   10 seconds ago   299MB
react-app    1         446feb548e5a   13 minutes ago   299MB
react-app    latest    446feb548e5a   13 minutes ago   299MB
ubuntu       latest    ba6acccedd29   3 days ago       72.8MB
alpine       latest    14119a10abf4   7 weeks ago      5.6MB
```

**How point the "latest" tag to the actual latest image?**

```sh
docker image tag d02 react-app:latest
react-app % docker images    
`=>                    
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
react-app    2         d02f199fb61c   About a minute ago   299MB
react-app    latest    d02f199fb61c   About a minute ago   299MB
react-app    1         446feb548e5a   14 minutes ago       299MB
ubuntu       latest    ba6acccedd29   3 days ago           72.8MB
alpine       latest    14119a10abf4   7 weeks ago          5.6MB
```

### Sharing Images

https://hub.docker.com/repositories

```sh
image tag d02 lawjune/react-app:2
react-app % docker images                           
REPOSITORY          TAG       IMAGE ID       CREATED          SIZE
lawjune/react-app   2         d02f199fb61c   8 minutes ago    299MB
react-app           2         d02f199fb61c   8 minutes ago    299MB
react-app           latest    d02f199fb61c   8 minutes ago    299MB
react-app           1         446feb548e5a   21 minutes ago   299MB
ubuntu              latest    ba6acccedd29   3 days ago       72.8MB
alpine              latest    14119a10abf4   7 weeks ago      5.6MB
```

```sh
docker login
```

```sh
docker push lawjune/react-app:2 
```

### Saving and Loading Images

```sh
docker image save --help
docker image save -o react-app.tar react-app:2
```

```sh
docker image load --help
docker image rm react-app:2
docker images
...
```
```sh
docker image load -i react-app.tar 
```

## Working with Containers

**IN THIS SECTION
* Starting & stopping containers 
* Publishing ports
* Viewing logs
* Executing commands in containers
* Removing containers
* Persisting data using volumes
* Sharing source code
**

### Starting Containers

```sh
docker run react-app
```

Or *de-attach* the container
```sh
docker run -d react-app 
docker ps
```

```sh
docker run -d  --name blue-sky react-app 
```

### Viewing the Logs

```sh
 logs --help  
`=>
Usage:  docker logs [OPTIONS] CONTAINER

Fetch the logs of a container

Options:
      --details        Show extra details provided to logs
  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g.
                       2013-01-02T13:23:37Z) or relative (e.g. 42m for 42
                       minutes)
  -n, --tail string    Number of lines to show from the end of the logs
                       (default "all")
  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g.
                       2013-01-02T13:23:37Z) or relative (e.g. 42m for 42
                       minutes)
```

```sh
docker images
`=>
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
react-app    latest    d02f199fb61c   47 hours ago   299MB
ubuntu       latest    ba6acccedd29   5 days ago     72.8MB
alpine       latest    14119a10abf4   7 weeks ago    5.6MB
```

```sh
docker logs -n 5 a04
`=>
  On Your Network:  http://172.17.0.2:3000

Note that the development build is not optimized.
To create a production build, use yarn build.
```

```sh
docker logs -n 5 a04
`=>
  On Your Network:  http://172.17.0.2:3000

Note that the development build is not optimized.
To create a production build, use yarn build.

(base) mac@madeMacBook-Pro react-app % docker logs -n 5 -t a04
2021-10-21T14:25:48.648697500Z   On Your Network:  http://172.17.0.2:3000
2021-10-21T14:25:48.648852400Z 
2021-10-21T14:25:48.648990600Z Note that the development build is not optimized.
2021-10-21T14:25:48.649379000Z To create a production build, use yarn build.
2021-10-21T14:25:48.649408000Z 
```

### Publishing Ports

```sh
react-app % docker run -d -p 80:3000 --name C1 react-app
```

### Executing Commands in Running Containers

```sh
docker exec C1 ls
`=>
Dockerfile
README.md
node_modules
package-lock.json
package.json
public
src
yarn.lock
```

```sh
docker exec -it C1 sh
```

### Stopping and Starting Running Containers

```sh
docker stop C1   
```

```sh
docker start C1
```
*`docker run` creates a new container*

### Removing Containers


```sh
docker rm C1 -f
```

```sh
docker ps -a | grep C1
```

```sh
docker prune
`=>
docker: 'prune' is not a docker command.
See 'docker --help'
(base) mac@madeMacBook-Pro react-app % docker container prune
WARNING! This will remove all stopped containers.
```

```sh
docker ps -a
```

### Containers File System

```sh
docker exec -it a04 sh
`=>
/app $ echo data > data.txt
/app $ exit
```
```sh
docker exec -it a04 sh
`=>
/app $ ls
Dockerfile         node_modules       public
README.md          package-lock.json  src
data.txt           package.json       yarn.lock
```

### Persisting Data using Volumes

```sh
docker volume
`=>
Usage:  docker volume COMMAND

Manage volumes

Commands:
  create      Create a volume
  inspect     Display detailed information on one or more volumes
  ls          List volumes
  prune       Remove all unused local volumes
  rm          Remove one or more volumes
```

```sh
docker volume create app-data
```

```sh
docker volume inspect app-data
`=>
[
    {
        "CreatedAt": "2021-10-23T01:31:54Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/app-data/_data",
        "Name": "app-data",
        "Options": {},
        "Scope": "local"
    }
]
```

```sh
docker run -d -p 4000:3000 -v app-data:/app/data react-app
`=>
0436c27ec77124cd8037c75d45686026b538bdd39fad5216b1bdf293b1da156a
```

```sh
docker exec -it 043 sh
/app $ cd data
/app/data $ echo data > data.txt
sh: can't create data.txt: Permission denied
/app/data $ cd ..
/app $ ls -l
total 1188
-rw-r--r--    1 root     root           197 Oct 19 14:39 Dockerfile
-rw-r--r--    1 root     root          3367 Oct 19 14:55 README.md
drwxr-xr-x    2 root     root          4096 Oct 23 01:31 data
drwxr-xr-x    1 app      app           4096 Oct 23 01:34 node_modules
-rw-r--r--    1 root     root        679372 Oct 19 13:22 package-lock.json
-rw-r--r--    1 root     root           813 Mar  5  2021 package.json
drwxr-xr-x    2 root     root          4096 Oct 19 13:44 public
drwxr-xr-x    2 root     root          4096 Oct 19 13:44 src
-rw-r--r--    1 root     root        507430 Mar  5  2021 yarn.lock
```
=> *Revise the Dockerfile*

```Dockerfile
FROM node:lts-alpine3.14
RUN addgroup app && adduser -S -G app app
USER app
WORKDIR /app
RUN mkdir data
COPY package*.json .
RUN npm install
COPY . .
ENV API_URL=http://api.appspot.com/
EXPOSE 3000 
CMD npm start
```

```sh
docker build -t react-app .
```

```sh
docker run -d -p 5000:3000 -v app-data:/app/data react-app
`=> 
54f439e12f01e1afe70aea46329332fc8b1ab4177063e072a4add084494d9d51
```
```sh
docker exec -it 54f sh
/app $ cd data
/app/data $ echo data > data.txt
```
```sh
docker exec -it 54f sh
/app $ cd data/
/app/data $ ls
data.txt
```

### Copying Files between the Host and Containers

```sh
 docker ps
 `=>
CONTAINER ID   IMAGE          COMMAND                  CREATED      STATUS      PORTS                    NAMES
54f439e12f01   react-app      "docker-entrypoint.s…"   4 days ago   Up 4 days   0.0.0.0:5000->3000/tcp   boring_greider
0436c27ec771   d02f199fb61c   "docker-entrypoint.s…"   4 days ago   Up 4 days   0.0.0.0:4000->3000/tcp   eager_leavitt
a0483d131454   d02f199fb61c   "docker-entrypoint.s…"   5 days ago   Up 5 days   3000/tcp                 elated_wozniak
```

```sh
docker exec -it 54f439e12f01 sh
/app $ echo hello > log.txt
/app $ exit
docker cp 54f439e12f01:/app/log.txt .
cat log.txt 
`=>
hello
```

```sh
echo hi > secret.txt
docker cp secret.txt 54f439e12f01:/app
docker exec -it 54f439e12f01 sh       
/app $ cat secret.txt 
hi
```

### Sharing the Source Code with a Container

**PUBLISHING CHANGES**
* For production: build a new image
* For development: create a mapping between the directory of host and container
	**HOST**:/project -> **CONTAINER**:/app

```sh
docker run -d -p 5001:3000 -v $(pwd):/app react-app
`=>
52cbe21ea3b8d05c0d141a8473f9e5aac1f04c48c87f838c86ed66dacba2a03e
```

```sh
docker logs -f 52c
```

## Running Multi-container Applications

**IN THIS SECTION
* Docker Compose
* Docker networking
* Database migration
* Running automated test
**

### Installing Docker Compose

https://docs.docker.com/compose/install/

```sh
docker-compose --version
`=>
docker-compose version 1.29.2, build 5becea4c
```

### Cleaning Up our Workspace

```sh
docker container rm -f $(docker container ls -aq)
docker image rm -f $(docker image ls -aq)
```

```sh
docker ps -a
`=>
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### The Sample Web Application

```sh
vidly % ls
`=>
backend			docker-compose.yml	frontend
```

```sh
docker-compose up
```

### JSON and YAML Formats

### Creating a Compose File

### Building Images

```sh
docker-compose build
```

```sh
docker-compose build --help   
`=>          
Build or rebuild services.

Services are built once and then tagged as `project_service`,
e.g. `composetest_db`. If you change a service's `Dockerfile` or the
contents of its build directory, you can run `docker-compose build` to rebuild it.

Usage: build [options] [--build-arg key=val...] [--] [SERVICE...]

Options:
    --build-arg key=val     Set build-time variables for services.
    --compress              Compress the build context using gzip.
    --force-rm              Always remove intermediate containers.
    -m, --memory MEM        Set memory limit for the build container.
    --no-cache              Do not use cache when building the image.
    --no-rm                 Do not remove intermediate containers after a successful build.
    --parallel              Build images in parallel.
    --progress string       Set type of progress output (auto, plain, tty).
    --pull                  Always attempt to pull a newer version of the image.
    -q, --quiet             Don't print anything to STDOUT
```

*For production*
```sh
docker-compose build --no-cache
```

### Starting and Stopping the Application

```sh
docker-compose up -d
```

```sh
docker-compose down
```

### Docker Networking

```sh
docker-compose up -d
`=>
Starting vidly_db_1 ... done
Starting vidly_backend_1 ... done
Starting vidly_frontend_1 ... done
```

```sh
docker network ls
`=>
NETWORK ID     NAME            DRIVER    SCOPE
ba3d8773fd83   bridge          bridge    local
14d7626e3363   host            host      local
5f721cd8d52b   none            null      local
4b18e080b069   vidly_default   bridge    local
```

```sh
docker ps
`=>
CONTAINER ID   IMAGE              COMMAND                  CREATED      STATUS              PORTS                      NAMES
566785c954c6   vidly_frontend     "docker-entrypoint.s…"   3 days ago   Up About a minute   0.0.0.0:3000->3000/tcp     vidly_frontend_1
51b4ef43f514   vidly_backend      "docker-entrypoint.s…"   3 days ago   Up About a minute   0.0.0.0:3001->3001/tcp     vidly_backend_1
88efef962bbc   mongo:4.0-xenial   "docker-entrypoint.s…"   3 days ago   Up About a minute   0.0.0.0:27017->27017/tcp   vidly_db_1
```

```sh
docker exec -it -u root 51b sh
ping frontend
`=>
PING frontend (172.18.0.4): 56 data bytes
64 bytes from 172.18.0.4: seq=0 ttl=64 time=0.486 ms
64 bytes from 172.18.0.4: seq=1 ttl=64 time=0.194 ms
64 bytes from 172.18.0.4: seq=2 ttl=64 time=0.099 ms
```

### Viewing Logs

```sh
docker-compose logs --help
`=>
View output from containers.

Usage: logs [options] [--] [SERVICE...]

Options:
    --no-color              Produce monochrome output.
    -f, --follow            Follow log output.
    -t, --timestamps        Show timestamps.
    --tail="all"            Number of lines to show from the end of the logs
                            for each container.
    --no-log-prefix         Don't print prefix in logs.
```


### Publishing Changes

### Migrating the Database

```sh
docker-compose down
```
```sh
docker volume ls  
`=> 
DRIVER    VOLUME NAME
local     32fb050e9dea71c55a11d339bac0e4eb82dc77695206004e9c63e2f1818123ed
local     39a8fe574c4455c7b8b1adc925defc147c22ef4ee17063de1d5e882889339235
local     589e2d4bb0c4da197286d6869806c49be5f07a71abecd4eb9c87e952335549d6
local     60477e99aa034ea78df5a0bebb0a3f29358224b8d6fb4553cfa1bd17b5867702
local     app-data
local     f7186877fd72cb61226f2e91c5fb3219cc5c02d3893c731c7636de8a90d51e5b
local     fad422fe9859f9a3f8a1ba2fadd6b0096374192ff245f5f7cb777c5be9f4cf33
local     vidly_vidly
```
```sh
docker volume rm vidly_vidly
```
```sh
docker-compose update 
```

### Running Tests

## Deploying Applications

### Deployment Options

**DEPLOYMENT OPTIONS
* Signle-host deployment
* Cluster deployment
**

**CLUSTER SOLUTIONS
* Dokcer Swarm
* Kubernetes
**

### Getting a Virtual Private Server

**VPS OPTIONS
* Digital Ocean 
* Google Cloud Platform (GCP)
* Microsoft Azure
* Amazon Web Services (AWS)
**

### Installing Docker Machine

https://github.com/docker/machine

### Provisioning a Host

### Connecting to the Host

### Defining the Production Configuration

### Reducing the Image Size


































