# DOCKER

**LIST RUNNING CONTAINERS** - `docker ps`  
**LIST ALL CONTAINERS** - `docker ps -a`  
**STOP A CONTAINER** - `docker stop [container id]`  
**REMOVE A CONTAINER** - `docker rm [container id]`
**LIST ALL IMAGES** - `docker image ls`  
**REMOVE AN IMAGE** - `docker image rm [image name]`  
**VIEW LOGS ON CONTAINER** - `docker logs [container id]`  
**DISPLAY CONTAINER INFORMATION** - `docker inspect [container id]`  
**DISPLAY SPECIFIC CONTAINER INFORMATION** - `docker inspect -f '{{.NetworkSetting.IPAddress}}' [container id]`

## How do I install docker?

- https://www.docker.com/get-started
- “download for mac”
- create and account
- “Get Docker”
- Download and Install Docker.dmg

## How do I run PostgreSQL in docker?

https://hackernoon.com/dont-install-postgres-docker-pull-postgres-bee20e200198

- **GET DOCKER**

  - specific tag: `docker pull postgres:[tag_you_want]`
  - lastest: `docker pull postgres`

- **CREATE A SPOT FOR IT TO STORE DATA**

  - `mkdir -p ~/Docker/volumes/postgres`

- **RUN A POSTGRES DOCKER CONTAINER**

  - `docker run --rm --name postgres-docker -e POSTGRES_PASSWORD=docker -d -p 5432:5432 -v ~/Docker/volumes/postgres:/var/lib/postgresql/data postgres`
    - **—rm** - automatically remove the container on stop
    - **—name** - the name for the container
    - **-e** - provide environment variables
    - **-d** - run in the background
    - **-p** - expose an internal port to the host format [host port]:[container port] example [1234]:[8080] makes docker port 8080 accessible to the host via port 1234
    - **-v** - mount a host volume to a location on the container (this makes data live beyond the life of the container)

- **CONNECT TO THE CONTAINER**
  - `psql -h localhost -U postgres -d [database-name] -p [port]`

## Start Container From Dockerfile

- cd to the directory containing the Dockerfile
- Create an image: `docker build -f Dockerfile -t [image-name] .`
- Run the image: `docker run -p 8080:8080 dockerservice`

## How do I communicate over the network between two docker containers?

- https://www.linode.com/docs/applications/containers/docker-container-communication/#connect-two-containers

- `docker run --link=[container name]:[desired host name] [container to run]`
  - i.e. `--link=test-container:database` == postgresql://database:5432
