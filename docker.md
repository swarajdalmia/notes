# Docker 

The notes are made primarily from [here](https://www.youtube.com/watch?v=fqMOX6JJhGo&t=68s).

## why does one need docker ?

- Compatibility matrix, for application stack requiring difference software's requiring different version of depencies, libraries and compatibility with different versions/types of OS, Everytime something changes, do through the same process of checking everything. 
- Very complex setup time for environment for new developers, often commands in the hundreds.
- different dev/test/prod envionments hence issues in knowning whether the app would run the same in different envionments.

## What can it do ?

- one can run each component in a seperate container, each with there seperate libraries and dependencies. Each on top of the same VM and OS.
- create the docker once and new developers can start working with a set of few simple commands 

## What are conatiners ?

- They are completely isolated environments. 
- They can have their own processes, network interfaces, mounts except they share the same OS kernel. 
- They existed from before but reauired low level programming. Docker helps with a high level interface. 

### OS Basics

An OS is typically made of an OS kernel and a set of software over it. The kernel is responsible for communicating with the underlying hardware. The linux kernel say is the same for different version of linus OS, but the software above that differs. Docker can run different OS's as long as the the OSs are based on the same kernel that docker is running on top of(of the underlying host).
So one won't be able to run a windows containers with docker on a linux machine/server.
However, sometimes a veitual machine might help sort that issue out for example in cases where one uses linux conatiner on windows kernel. 

Hypervisors are tools with which one can run different OS's and kernel systems on the same hardware. They offer a more powerful way to conatinerize. 

That is the difference between **virtual machines and containers**. Docker runs on top of the OS kernel and has containers on top. While, a hypervisor runs on top of the hardware and carries on top of it virtual machines(which contain the OS as well). Docker conatiners are much smaller in size. Docker has less isolation as compared to VM's. A lot of the times, both of them are used together to use advantages of both. 


### Container vs Image 

An image is a package or template that is used to make containers. Conatiners are running instances of images.  

Docker is very helpful in **DevOps** and reduces the the issues between the developmet and production teams. 
 
## Docker : Getting Started 

Docker has a community edition and an enterprise edition(lot of other functionalities). Here, the community verison is discussed further. 

## Docker on MAC 

One can use either Docker toolbox or docker desktop. Docker desktop is the newer way. Docker on mac creates a linux system underneath, but it is created on hyperkit instead of oracle virtual box. This is done to run a linux container on Mac. There are no(if any) mac based images or containers.

Look [here](https://docs.docker.com/docker-for-mac/install/) on how to install.


### Filesystem and Storage on MAC

Docker is not natively compatible with macOS, so Hyperkit is used to run a virtual image. Its virtual image data is located in:  
```
~/Library/Containers/com.docker.docker/Data/vms/0
```
Within the virtual image, the path is the default Docker path `/var/lib/docker`.

You can investigate your Docker root directory by creating a shell in the virtual environment:
```
$ screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty 
```
You can kill this session by pressing Ctrl+a, followed by pressing k and y.

More info on storage and paths in docker can be found [here](https://www.freecodecamp.org/news/where-are-docker-images-stored-docker-container-paths-explained/).

## Example : Pulling and running a docker image

Pull and run the whalesay image from [docker hub](https://hub.docker.com/r/docker/whalesay) and simply run the command in terminal. 

## Docker Commands 

- docker run : runs a conatiner from an image. If an image is not present locally it is pulled from docker hub, However, this is done only once. If the image has already been pulled, it will be reused. 

- docker ps -a : lists all running containers and basic info about them. -a lists not only the containers that are running but also ones that have recently finished running. 

- docker stop \<name/id\> : used to stop the running of a container. When one is proving an id, even a few digits work as long as there is uniqueness. 

- docker rm \<name/id\> : completely removed a container 

- docker rmi \<name/id\> : removes the docker image. But before doing that one must delete all the dependent containers to remove an image. How does one find, which containers have a dependeny on an image.  

- docker pull \<name\> : pulls a docker image from docker hub. The run command implicitly does that and creates a conatiner. 

- docker images : displays all the docker images present in the computer. 

A container only lives as long as the process inside it is alive. This is why the whalesay container doesn't dhow up on docker ps. 


### Appending commands 

- To do : prive example/explanations

### Execute a command : on a running container 

- docker exec \<command-name\> cat \<flie-location\> : it executes a command on a running contianer. 

### Docker Run - attach and detach
 
In a normal run, it is by default in attach mode. In this mode, one can not do anything in that console until the container is finished running. executing ctrl+c option, stops running the container. 

```
docker run -d <name>
```

Runs a container in detach mode s.t. it executes in the background and one gets back to the prompt immediately. Ater running in detach mode, one can use docker attach \<name\> to get back to attach mode. 

 
### Run : tag 

on executing the following: 
```
docker run redis
```
The latest version of the software redis is pulled. The default tag is latest. If one wants to download an earlier version one needs to specify it as : 
```
docker run redis:4.0
```
Every image in docker hub, has multiple tags in the description. 


### Run - STDIN 

By default, docker doesn't listento a standard input. It runs in a non-interactive mode. 
To run it in interactive mode one has to specify the -i parameter.
```
docker run -i <name> 
```
-t standard for pseude terminal and normally they are used together(-it) to ensure input is given to the docker container and -t can help specify a terminal to interact in. 

### Run - PORT mapping 

The underlying host in which docker is installed is called the Docker Host. The post on which the app is running is displayed on the run command. Every docker container has a default IP assigned and is only accessible in the docker host i.e. it is an internal IP. To communicate with users outside, one needs the IP of the docker host. For it to work, one needs to map the container in the docker host to the host in the container using 'docker run -p' command. This wasy multiple instances of the app can be run in different hosts/containers which are connected to different ports. 

### Run - Volume mapping 

Say, one runs a docker container and the program creates a lot of data which is stored within the file system of the container. However, if one removes the container, all the data will be deleted as well. To prevent that from happening one can use 'docker run -v' command to map the data folder in the container to one outside. This way all the data will be stored outside on the host. 

### Inspect container 

```
docker inspect <name/id>
```

gives more information than ps, like, states, mmounts, config data etc. 

### Container logs 

```
docker logs <name>
```

## Environment Variables
 
Useful if one wants to specify variables without changing the code. A good way is to instead use an envionment variable which can be specified when the docker run command is used. 
```
color = os.environ.get('APP_COLOR')
```

Now, one can specify the envionment variable color with -e shown below :
```
docker run -e APP_COLOR=blue <name>
```

### Inspect Envionment Varibles 

To inspect the environment variables of a running container one can use docker inspect. There is an env\_var under config. 

## Creating : Docker Images

How to create a docker image ?

TODO.(try creating a docker image for a project)

Creating a docker image uses Dockerfile which carries the instructions on creating the docker image. 

```
docker built Dockerfile -t <tag>
```
The above command creates an image with tag with the instructions from Dockerfile. 
Use docker push to make it available in docker hub.

### Dockerfile

It is a text file written in a specific format that docker can understand. 
It's format is INSTRUCTION(left and in caps), the part on the right are the instructions. 

The start must specify a base OS or another image (FROM instruction).

ENTRYPOINT helps specify a command that will be run when we run the image as a container. 

### Layered Architecture 

The Dockerfile instructions creates the docker image  in a layered architecture and each layer stores the changes from the last layer.

One can also start the built from specific layers/steps instead of failure of some intermediate steps. All the layers built are cached. If one rebuilts again, docker uses the cached layers. 

This is useful when one changes the source code. In this case, on the layers including and below the source code need to be rebuilt.

Even when a different container is built, it will reuse layers from the cache that were saved for other containers.

## Docker : Commands, Arguments and EntryPoint

When one locked at the Dockerfile for a doker image, one can see the CMD command which specifies the process/program that is run when the container starts. When one runs a container with ubuntu OS, the container ends since the CMD command runs bash and bash needs a terminal but none is found and therefore it exits. 

To specify a different command to run when a container is run, one way is to append a command. Example: 

```
docker run ubuntu sleep 5
```
However to permanently do this, one can make a new image from the base Ubuntu image and add the new `CMD sleep 5` line. Incase one wants a user specified time instead of 5 one can use `ENTRYPOINT["sleep"]` command instead of the CMD line. Sometimes its important to specify parameters in JSON format. 

## Docker : Networking 

On installing docker by default it creates 3 networks automatically: brudge, none, host.
By default each container attaches to the bridge and they get an internal IP address with which they can access each other. To acess from outside, we map these IP's to ports on the docker host. Another way to communicate externally is to set `--network=host` on docker run. If this is donee, no port mapping is required. However this might have some issues in the case of running multiple instances of the same image.
 
By setting `--network=none` the containers run in an isolated network and don't have any access to internal/externl networks. 

### User-defined networks 

By default all containers when connected to the default network 'bridge' are connected amonsgt themselves. By feault there is therefore on;y 1 bridge network, however it is possible to create user defined bridge networks too using `docket network create`. 

One can use `docket network ls` to list all the networks in docker. However, how does one see the IP's ? One can check it using `docker inspect <name/id>` and find the IP under Networks in the JSON. If connected to each other, the containers can access each other using both the IP addresses, however the conatiner might get a different IP when the system reboots, therefore the best way to do it is using the container names. 

Docker has a built in DNS serves which helps resolve these using the conatiner name.

How does docker implement networks internally ? 

Docker uses namespaces and creates a namespace for every container. It uses virtual ethernet pairs to connect containers. 

## Docker Storage Drivers and Filesystems 

When docker is installed, it creates a folder structure at `var/lib/docker` (seperate for max/windows). Look at the link under Mac heading to find further info. Each docker image has layers, which can't be modified unless one rebuilts the image. When a container is built from an image, another layer layer is added which is writable which is used to store data created by the container. This layer only exists as long as the container is alive. The same image layer is shared by all containers created from the image. The image layer is read only while the container layer is writable. On editing a file in a container, docker **copies on write** i.e. creates a copy of the source code from the image layer onto the container layer and modifications are made there and that overrides the copy in the image layer. 

### Volumes

Usually, the data that is created by a container process is saved within and it is lost when the conatiner is lost, however it possible to save the data in a volume by specifying `docker run -v` which mounts the data to a volume folder outside the container which is on the docker host. 

There are two types of mounting: volume mounting and bind mounting. Volume mounting mounts a folder in the volume sub directory under /var/lib/docker directory and bind mounting mounts a subdirectory any whether in the system. 

Using -v is the old style and the newer style is `--mount`. Docker uses storage drivers to enable layered architecture. 


## Docker Compose

Requires knowledge of YAML. Normally when setting up a container,one used `docker run` for various libraries/packages. Instead of doing that it is useful to speciify a YAML file and use `<filename> up` to set up a container. 

When one runs a lot of containers and wants to specify ports and link the containers together, its simpler to use a docker compose yml file. Check 1:26:30 of [video](https://www.youtube.com/watch?v=fqMOX6JJhGo&t=68s) for an example. One can also build an image from a code folder in the yml file. One can also specify a network and make connections through the YML file. 

## Docker Registry 

When say one runs `docker run nginx`, nginx is the name of an image. When nginx is written it means nginx/nginx, which correspons to `<user/account name>/<image/repository name>`. These images are by default pulled from docker hub, the name for which is 'docker.io'. gcr.io is google's registry that has a lot of kubernetes stuff. 

 
Private registry - lots of websites provide private registries. One needs to login first via the terminal to use them. It is possible to deply ones own private registry too, on the docker host. 
Look at 1:38:50 in the link.

## Docker Engine 

A docker engine is simply the host with docker running on it. 
When one installs docker on linux, 3 things are installed: Docker Deamon(manages docker objects), REST API(communication between programs and the deamon) and Docker CLI(cmd line interface). The CLI can be on another host too and one can specify the remote host with -H flag.

Docker uses namespaces to isolate workspace and ensure containerization. 

### cgroups 

Since the containers and the host share memory and CPU of the host. It is possible the container might over utilize these resources. Docker used cgroups to limit usage. An example of setting a limit of max:50% for a CPU is `docker run --cpus=.5 ubuntu`, or `docker run --memory=100m ununtu`.

