# udemy_DockeryAndKubernetes

Udemy: [course](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)

## Handy Generic Commands (from bash shell)
```cmd
# Find all node_module directories
$ find . -type d -name 'node_modules'

# Delete all node_module directories
$ find . -type d -name 'node_modules' -exec rm -rv {} \;
```

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
$ docker run -p 3000:3000 -v /app/node_modules -v //c/git/Udemy/udemy_DockeryAndKubernetes/my-code/Section6-workflow/frontend:/app mkozi/frontend

# MINW64 Git bash has issue with windows paths, the following works:
$ MSYS_NO_PATHCONV=1 docker run -p 3000:3000 -v /app/node_modules -v /c/git/Udemy/udemy_DockeryAndKubernetes/my-code/Section6-workflow/frontend:/app mkozi/frontend

# run the tests (alternate is to add service to docker-compose.yml)
$ MSYS_NO_PATHCONV=1 docker run -p 3000:3000 -v /app/node_modules -v /c/git/Udemy/udemy_DockeryAndKubernetes/my-code/Section6-workflow/frontend:/app mkozi/frontend
# in separate terminal
$ docker ps  # get docker id
$ docker exec -it <container id> npm run test

# two phase nginx prod docker build (run from the Section6 frontend directory)
$ docker build -t frontend-prod .
$ docker run -p 8080:80 <image-id>
```

## Section 7

### Resources

* Travis CI: [site](https://travis-ci.org/)

## Section 8

### Command

```cmd
# from the Section8-Multi-Container root directory:
$ docker-compose up --build

# when done:
$ docker-compose down
```

## Section 12

### Commands

```cmd
# pod only used in development
$ kubectl apply -f client-pod.yaml
$ kubectl apply -f client-node-port.yaml
$ kubectl get pods
$ kubectl get services

$ kubectl describe pod client-pod

$ kubectl delete -f client-pod.yaml

# deployment can be used for dev or production
$ kubectl apply -f client-deployment.yaml

$ kubectl get pods -o wide

# update to a new version of the image
$ kubectl get deployment
$ kubectl set image deployment/client-deployment client=mkozi/multi-client:v5
$ kubectl describe pod <pod-name>

# misc
$ kubectl logs <pod-name>
$ kubectl exec -it <pod-name> bash
```

## Section 14: Multi-container app in kubernetes

ingress-nginx: [github](github.com/kubernetes/ingress-nginx) | [docs](https://kubernetes.github.io/ingress-nginx/) | [manditory yaml](https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml)
Kubernetes Ingress System: [blog](https://www.joyfulbikeshedding.com/blog/2018-03-26-studying-the-kubernetes-ingress-system.html)
kubernetes documentation: [kubernetes.is](https://kubernetes.io/)

```cmd
# can apply all files in a directory (such as k8s)
$ kubectl apply -f k8s

$ kubectl get storageclass
$ kubectl describe storageclass

$ kubectl get pv
$ kubectl get pvc

$ kubectl create secret generic pgpassword --from-literal PGPASSWORD=password123

# nginx ingress
# https://kubernetes.github.io/ingress-nginx/deploy/#prerequisite-generic-deployment-command
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
$ kubectl get svc -n ingress-nginx

```