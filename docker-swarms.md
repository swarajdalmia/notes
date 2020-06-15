# Docker Swarms 

A brief introduction of docker swarms.

## Container Orchestration

It is used for container orchestration. Consider when there are multiple users, then one needs to deply multiple instances of an application. One needs to keep a watch over the load and states of the containers(incase they fail) and the health of the host itself. One needs to monitor the health of the containers and the host itself. 

Container orchestration is a solution that consists of a set of tools and scripts which helps. One can create 1000's of instances of application with a single command. 

Some of the container orchetration tools out there currently are docker swarm, kubernetes(google), mesos(apache?). Mesos is difficult the start up, kubernetes is the most popular one out there, docker swarm is the easiest.  

## Docker Swarms 

- Setup : requires multiple hosts, one of which is the swarm manager. Run the `docker swarm init` command on the manager and on the other hosts one runs `docker swarm join --token <token>`. The workers are also refered to as nodes. 

- Docker service is an instance of a service that runs across worker nodes. An example would be to run the command `docker service create --repilcas=3 my-web-server` in the swarm manager host. The docker service automatically deals with distribution, so instead of docker run, one executes docker service create.  






