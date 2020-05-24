# docker

## CLI
- show running containers:
  - docker ps
- show all containers: 
  - docker ps -a
- run one-time command in the container
  - docker run busybox ls
  - docker run = docker create + docker start
- start shell within a new container
  - docker run -it busybox sh

- remove unused containers and images
  - docker system prune

# executing commands in running container
- terminal 1:
  - docker run redis
- terminal 2:
  - docker exec -it <containerId> redis-cli
- docker exec -it <containerId> sh





# build container and push it to dockerhub
sudo docker build -t paladinze/react_playground -f Dockerfile .
sudo docker push paladinze/react_playground:latest


# run containers using docker-compose
docker-compose up -d

# run containers & rebuild the images
docker-compose up -d --build


# run mysql container
docker run --name mysql -e MYSQL_ROOT_PASSWORD=921021 -d -p 3306:3306 -v mysql_data:/var/lib/mysql/data mysql

# run postgres container
docker run --name postgres -e POSTGRES_PASSWORD=921021 -d -p 5432:5432 -v postgres_data:/var/lib/postgresql/data postgres

# generate encrypted docker hub password in travis
travis encrypt REGISTRY_PASS=Zfmttm01 --add env.global



/********************************************
Basic Commands

// get container's volume
inspect -f '{{ .Mounts }}' containerid

// stand up a container
docker run -d -p 80:80 --name webserver nginx

// stop a running container
docker stop webserver

// list local images
docker images

// build image
docker build -t friendlyhello .
docker run -p 4000:80 friendlyhello

// remove abandoned containers
$ docker rm $(docker ps -a -q -f status=exited)

// remove exited containers
$ docker rm $(docker ps -a -q -f status=exited)

/********************************************
Publish to docker to Publish Registry
********************************************/

// tag an image to be published to registry
docker tag friendlyhello john/get-started:part1

// publish the image to registry
docker push john/get-started:part1

docker run -p 4000:80 username/repository:tag


/********************************************
Install Docker
********************************************/
https://store.docker.com/editions/community/docker-ce-desktop-mac

/********************************************
Back & Restore data volume (ghost as example)
********************************************/
# deploy ghost
docker run -d --name robot_blog -p 2368:2368 ghost:1.16

# deploy ghost from existing data container
docker run -d --name myGhost -p 80:2368 --volumes-from data_ghost ghost:1.16

# create backup tar for volume
docker run --rm --volumes-from <container_id> -v $(pwd):/backup busybox tar cvf /backup/<backup_name>.tar /var/lib/ghost/content

# create a new data container
docker create -v /var/lib/ghost/content --name data_ghost busybox

# extract the backup into the new data container
docker run --rm --volumes-from data_ghost -v $(pwd):/backup busybox tar xvf /backup/backup.tar

# start app container from the new data container
docker run -d --name myGhost -p 80:2368 --volumes-from data_ghost ghost:1.16


## three levels of file system

- readonly level
- init level
- read/write level
