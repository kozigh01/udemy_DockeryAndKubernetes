# udemy_DockeryAndKubernetes
Udemy: [course](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)

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