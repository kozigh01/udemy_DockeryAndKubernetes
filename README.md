# udemy_DockeryAndKubernetes

Udemy: [course](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)

## Basic Docker Commands

### Run Commands

```cmd
$ docker run hello-world        # pull image from docker hub and run

$ docker run -it alpine sh      # run the alpine image and over-ride the default command with 'sh'

$ docker run -d redis           # pull image from docker hub and run in the background
$ docker container ls           # see the running container
$ docker ps                     # see running docker processes (looks like docker container ls)
$ docker exec -it <container-id> bash   # run a 2nd command (bash) in running container
$ docker stop <container-id>    # stop docker container gracefully
$ docker kill <container-id>    # stop docker continer immediately
```

### System Commands

```cmd
$ docker system df              # show docker related file system resources
$ docker system prune --all     # remove docker resources from file system
```

### docker-compose

```cmd
# in a directory with a docker-compose.yml file:

$ docker-compose up     # start the containers defined n the docker-compose.yml file
$ docker-compose down   # stop the containers that were started with docker-compose up

$ docker-compose up --build     # force rebuild of docker files

$ docker-compose up -d      # start containers per docker-compose.yml in the background
$ docker ps                 # see running containers
$ docker logs <container-id>    # see output from container running in background
$ docker-compose ps         # see status of containers in docker-compose file
$ docker-compose down
```

## Section 3

### Commands

```cmd
# basic build
$ docker build .

# tagged image
$ docker build -t mkozi/my-redis:1 .

# create image from container
$ docker run -it alpine sh
/ # apk add --update redis

-- open 2nd terminal, and run:
$ docker ps
$ docker commit -c 'CMD ["redis-server"]' c4ddef839cf8
```

## Section 4

### Commands

```cmd
$ docker build -t simpleweb .
$ docker run -p 8080:8080 simpleweb
```

## Section 5

### Commands

```cmd
$ docker-compose up
or
$ docker-compose up --build
```

## Section 6

### Resources
* Create React App (npx): [quick start](https://create-react-app.dev/docs/getting-started/#quick-start)

### Commands
```cmd
$ docker build -f Dockerfile.dev -t mkozi/frontend .

$ docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app mkozi/frontend
$ docker run -p 3000:3000 -v /app/node_modules -v //c//git//Udemy//udemy_DockeryAndKubernetes//my-code//Section6-workflow//frontend:/app mkozi/frontend

# MINW64 Git bash has issue with windows paths, the following works:
$ MSYS_NO_PATHCONV=1 docker run -p 3000:3000 -v /app/node_modules -v /c/git/Udemy/udemy_DockeryAndKubernetes/my-code/Section6-workflow/frontend:/app mkozi/frontend
```
