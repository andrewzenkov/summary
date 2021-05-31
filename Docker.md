Running image is container.


`docker run -i debian`: run and go to process <br>

`docker ps`: list of running containers <br>
`docker ps -a`: show all available containers <br>

`docker commit ID_CONTAINER NAME_IMAGE` <br>
`docker inspect IMAGE_NAME`: Provide detailed information on image <br>

`docker rmi DOCKER_NAME` <br>
`docker build .` <br>
`docker build --no-cache=true` <br>

ONBUILD COPY package.json /usr/src/app
ONBUILD RUN npm install
ONBUILD COPY . usr/src/app

`docker run -d -p 4000:3000 IMAGE_ID`: (`-d` run in background, `-p` ports)

Dockerfile
---

```
1. COPY . usr/src/app
2. WORDIR usr/src/app
3. RUN npm install 
4. CMD [‘npm’, ‘start’] 
```
3. will be run when build image
4. will be run when run image (container)
---

To put env variables dynamically use `-e` flag. <br>
Example: `docker run -it -p 4000:3000 -e APIHOST=1000 IMAGE_NAME`

Create variables in docker

```
1. FROM node:14-onbuild
2. COPY . usr/src/app
3. RUN npm install
4. ARG PORT=1234

5. EXPOSE $PORT 
6. ENV PORT $PORT

7. CMD [npm’, ‘install’]
```

4. This is variable port will be default if we didn’t receive it
5. What port will be available, use variable from arg
6. Will use arg variable for PORT variable

---

`docker exec` to connect to container


`Docker run` - for new container
`Docker start` - for already existed 


<h4>Container should be ephemeral (shouldn’t store a state)</h4>

Each command in dockerfile creates a new layer. If we want to avoid creating a new one we can use && ( \ - just for line replacing and move it on a new one).

```
RUN go get -d -v golang.org/x/net/html \
  && CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .
```
  
By default if we run `-it` flag it runs node. In majority of cases we need bash and we need to add `/bin/bush`

Example: `docker run -it myappimage /bin/bash`

`RUN apk update && apk add bash`: helps to install bash.

`docker system prune -a`: to delete all all unused images and containers
