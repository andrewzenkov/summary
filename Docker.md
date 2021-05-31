Running image is container.


`docker run -i debian`: run and go to process <br>

`docker ps`: list of running containers <br>
`docker ps -a`: show all available containers <br>

`docker commit ID_CONTAINER NAME_IMAGE` <br>
`docker inspect IMAGE_NAME`: Provide detailed information on image <br>

`docker rmi DOCKER_NAME` <br>
`docker build .` <br>

ONBUILD COPY package.json /usr/src/app
ONBUILD RUN npm install
ONBUILD COPY . usr/src/app

`docker run -d -p 4000:3000 IMAGE_ID`: (`-d` run in background, `-p` ports)

Dockerfile
---

COPY . usr/src/app (don’t forget to add .dockerignore and put node_modules)
WORDIR usr/src/app
RUN npm install (will be run when build image)
CMD [‘npm’, ‘start’] (will be run when run image (container))

---

To put env variables dynamically use -e flag. Example:
docker run -it -p 4000:3000 -e APIHOST=1000 IMAGE_NAME


Create variables in docker

FROM node:14-onbuild
COPY . usr/src/app
RUN npm install
ARG PORT=1234 (this is variable port will be default if we didn’t receive it)

EXPOSE $PORT (what port will be available, use variable from arg)
ENV PORT $PORT (will use arg variable for PORT variable)

CMD [npm’, ‘install’]


And for using it we need write for example this one:

docker build -p 4000:3000 DOCKER_ID --build-arg PORT=4444 .

Docker compose - util which helps to resolve the problem of communication between containers.


‘docker exec to connect to container


Docker run - for new container
Docker start - for already existed 


Container should be ephemeral (shouldn’t store a state)


docker build --no-cache=true


dot in the end of command means to start it in current directory



Each command in dockerfile creates a new layer. If we want to avoid creating a new one we can use && ( \ - just for line replacing and move it on a new one).
RUN go get -d -v golang.org/x/net/html \
  && CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .
By default if we run -it flag it runs node. In majority of cases we need bash and we need to add /bin/bush 

Example: 
docker run -it myappimage /bin/bash

Also you need to install bash by (add line in docker ‘RUN apk update && apk add bash’)
docker system prune -a / to delete all all unused images and containers
