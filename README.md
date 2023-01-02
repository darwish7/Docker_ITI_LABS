# Docker_ITI_LABS

## lab2

###### problem1 

```
docker build -t lab2:v1.1 . 
docker run -d --name ziadcontainer2 -p 9890:80 lab2:v1.1
docker exec -it ziadcontainer2 bash
```
###### problem2 
using single stage

touch Dockerfile
```
FROM node:18.12.1

	WORKDIR /myapp

	COPY . .

	RUN npm install 

	EXPOSE 3000

    CMD ["npm","start"]
```
```
sudo docker build -t myapp:v1.0 .
sudo docker run -d --name reacttest -p 9090:3000 myapp:v1.0
```

using multi-stage dockerfile

touch Dockerfile
```
FROM node:18.12.1 AS build 

	WORKDIR /myapp

	COPY . .

	RUN npm install 
	RUN npm run build

	FROM nginx:alpine
	COPY --from=build /myapp/build /usr/share/nginx/html
	EXPOSE 80
	ENTRYPOINT ["nginx","-g","daemon off;"]
```
```
sudo docker build -t myapp:v1.2 .
sudo docker run -d --name reacttest5 -p 9091:80 myapp:v1.2
```
###### problem4 

```
sudo docker network create myNetwork
sudo docker run -d --name cont1 -p 8001:80 ubuntu
sudo docker run -d --name cont2 -p 8002:80 ubuntu
sudo docker network connect myNetwork cont1
sudo docker network connect myNetwork cont2
```
from one container we run
```
apt update
apt install curl
curl test2
```

## lab3
###### problem1 

we create docker-compose.yml with the following
```
version: "3.8"
services:
  test_compose:
      container_name: ziadcontainer3
      image: myapp:v1.2
      ports:
        - "3000:80"
```
then we run `> docker compose up`

###### problem2
files are in the repo 


important link from the docker documentation to test the docker compose:
[docker compose](https://docs.docker.com/compose/gettingstarted/).

