## Docker commands

1. `docker --version` - returns the version of installed docker
2. `docker pull 'image_name'` - pulls the image from docker hub. image_name has to be valid image name from the docker hub repository.
3. `docker run 'image_name'` - runs the image as a container. 'image_name' has to be valid image name.
4. `docker images` - displays the currently installed images on the system.
5. `docker rmi 'image_id'` - deletes the installed image.
6. `docker images -q` - displays the ID's of installed images.
7. `docker inspect 'image_name'` - displays the details of image.
8. `docker ps` - display the list of currently running containers.
9. `docker ps -a` - display the list of all containers in the system
10. `docker history 'image_id'` - displays the history(all the ran commands) of that container
11. `docker top 'container_id'` - displays the top processes within that container
12. `docker stop 'container_id'` - stops the running container
13. `docker rm 'container_id'` - deletes the container
14. `docker stats 'container_id'` - display the stats of running container(cpu and memory utilization)
15. `docker attach 'container_id'` - attaches to a running container
16. `docker pause 'container_id'` - pauses the running container
17. `docker unpuase 'container_id'` - unpauses the running container
18. `docker kill 'container_id'` - Kills the processes in a running container
19. `docker container exec -it container_name bash` - open the container image in interactive mode

### Docker build

`docker build -t image-name:tag_name dir`

1. -t - to mention a tag to the image
2. image-name - name of the image which we are going to build
3. tag_name - tag you want to give to your image
4. dir - directory path where the Dockerfile contains

official docs reference - https://docs.docker.com/get-started/04_sharing_app/

Example 1:
`> docker build -t="mywebserver" .`

### Publishing docker image

1. create the repository in the docker hub
2. copy the push command
3. login to the docker in your host machine using `docker login` command
4. use the `docker tag` command to give the local image a new name.
5. Then try to push the command.

### Example commands for pushing repo to hub

1. `docker login -u 201996` - command used to login to docker hub. prompts for password
2. `docker tag docker-test 201996/test-docker` - updates the name of the local image(docker-test) to 201996/test-docker.
3. `docker push 201996/test-docker` - pushes the image to remote.

### Mapping a port

1. `docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins` - 8080:8080 is the host port number. 50000:50000 is the docker container port number
2. To find the port number use the `docker inspect jenkins/jenkins` command.

### Private registries

1. `sudo docker run –d –p 5000:5000 –-name registry registry:2`
2. use the above command to download the private registry
3. `-d` - runs the container as a service
4. `-p` - maps to the port 5000
5. `docker ps` - to check wether the registry is running
6. `docker tag 17b5c2fe188c localhost:5000/test-docker` - tag one of the existing image
7. `docker push localhost:5000/test-docker` - push the local image to private repository
8. `docker pull localhost:5000/test-docker` - pull the local image to private repository

### Sample Docker compose file

```
version: "2"
services:
  databases:
    image: mysql
    ports:
      - "3306:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_USER=user
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=demodb
  web:
    image: nginx

```

1. databases and web are two different services
2. ports are mysql ports
3. environment section holds the env variables
4. `docker compose up -d` - runs the application stack in the background

### Sample Dockerfile

```
# This is a test image
FROM ubuntu
MAINTAINER shiva@gmail.com

RUN apt-get update
RUN apt-get install -y nginx
CMD ["echo", "Image Created"]
```
