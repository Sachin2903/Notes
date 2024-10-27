                Docker

# MIcrosystem & containerization - Docker

# Container
Containers are software that wrap up all the parts of a code and all its dependencies into a asingle deployable unit that can be used on different system and servers.

>> Multiple isolated container can be launched together to form micoservices which cab be easily managed using any orchestration tool eg. docker swarm, kubernetes  etc

## Container vs Vm
* container
1. container only the bare minmum parts of the os required to run the software updates are easy and simple to do.
2. this isolation provided by a container isn't as complete as of a VM but is adequate
3. container are self contained environments that can easily be used on different os 

* Vm
1. contains the complete os that is normally used on system for general purpose UPdates are time consuming and tough.
2. VM provides complete isolation from the concerning host system and is also more secure
3. Vms aren't that easily ported with the same settings from one os to another.



![Alt text](../../Pictures//DOCKER%20Full%20Course%20in%20HINDI%20_%20Docker%20Tutorial%20for%20beginners%20in%202022%20_%20Docker%20Compose%20_Great%20Learning%2017-55%20screenshot.png)

## Docker install

1. Install Docker CE
sudo apt update 
sudo apt install docker.io

sudo apt remove docker.io -y

docker --version

2. Set up the docker reposiitory
-> sudo apt-get / apt update

This command refreshes the list of available packages and versions on your system. It ensures you’re getting the latest versions of packages from your repositories.

-> sudo apt install apt-transport-https ca-certificates curl software-properties-common

This installs essential tools:

apt-transport-https allows using HTTPS to fetch packages.
ca-certificates manages certificates to enable secure communication.
curl helps transfer data from or to a server.
software-properties-common provides tools to manage software repositories.

-> curl --fsSl https://download.docker.com/linux/ubuntu/gpg | sudo apt add -
or
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /usr/share/keyrings/docker-archive-keyring.gpg


This downloads Docker’s GPG key and adds it to your system to verify the packages you download from Docker. The key ensures that packages are authentic and haven’t been tampered with.


-> sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

--> sudo apt-get update 
--> sudo apt-get install docker-ce


## Docker environment
1. Docker engine 
2. Docker object
3. Docker registry
4. Docker compose
5. Docker swarm

### Docker engine 
Docker engine is as the name suggests, its technology that allows for the creation and management of all the docker processes. the has three major parts to it.

docker cli --> docker api --> docker daemon

### Docker object
1. docker images
2. docker containers
3. docker volumes
4. docker networks
5. docker swarm nodes & services

1. docker images
docker images are set of instructions that are used to create containers and execute code inside it

>> sudo docker pull ubuntu
>> sudo docker images
>> sudo docker run --it -d --name -p 80:80 container_name ubuntu( image_name )

3333:4444
The first 3333 (before the colon) is the port number on the host machine.
The second 4444 (after the colon) is the port number inside the container.

-it: For interactive use (access container shell).
-d: For running the container in the background.
>> sudo docker ps ( running container )
>> sudo docker ps -a ( to see all container )


--> to inside a container
>> docker exec -it container-name / container_id bash

--> linux command
>> service nginx status 
>> service nginx start

--> stop container
>> docker stop container_id

--> stop container forcefully
>> docker kill container_id

--> restart the contaier
>> docker restart container_id / container_name 

--> remove a container
>> docker rm container_id

--> remove a container forcefully 
>> docker rm  -f container_id

--> create a new image with cuurent container state , to persisit the configuration
>> docker commit container new_image_name

### docker volumes
docker volumes are basically persistent storage locations for the containers. they can be easily & safely attached and removed from different container. And they are also portable from system to another 

volumes drivers allow you to perform unique abilities such as creating persistent storage on other hosts, cloud, encrpt volumes they basically enhance the abilities of a volume.

## docker networks
a docker networks is basicallty a connection between one or maore container one of the more powerful thinfs about the docker container is the they can be easult connected to one other and even other software, this makes it very easy to isolate and manage the containers

### docker registry
can think of registries as storage locations for docker images these images can be versioned in the registry as well.

ECR , DOCKER HUB , AZURE CONTAINER REPO






