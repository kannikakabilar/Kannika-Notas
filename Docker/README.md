**What is Docker?**

A tool that helps developers create, deploy, and run applications inside "containers." It's like a lightweight process, that holds everything an application needs to run, including code, libraries, and system tools independent of environment.

**Pros:**
- helps automate builds
- security through isolation of process and file system
- verson control
- ci/cd

**Cons:**
- storage for data
- monitoring status

Components of Docker:
- Docker Enginer: it is the interface that allows you to create, run, manage containers - main software to use for running docker containers
- Docker Images: a light-weight package that contains everything needed to run an application - the code, dependencies - built using the Dockerfile
- Docker Container: when you run an image, you create an instance of the image which is the docker container, it runs the executed application

**Registry**
Docker’s public registry is called Docker hub, which allows you to store images privately. In Docker hub, you can store millions of images.
- docker push myorg/img
- docker pull myorg/img

- Docker Compose: helps manage multi-container docker image with docker-compose.yml
Services: Each container that your application needs (like a web server, database, etc.).
Networks: How the containers communicate with each other.
Volumes: Where data is stored and how it's shared between containers.

States of a Docker Container:
- docker ps // shows all running containers
- running, paused (temporarily halted), stopped
- docker start <container_name>
- docker stop <container_name>
- docker kill <container_name>

- sudo docker run -i -t alpine /bin/bash // run image as container

**Hypervisor** is like vmware that allows to run other OS while while docker uses Docker engine

When container is deleted, data is lost => **Docker volumes** to save the data

CMD vs ENTRYPOINT
- CMD: used for executing commands before the build inside the container environment
- ENTRYPOINT: initiate the build commandand make the container into an executable

docker run: run the docker image as a docker container.
docker ps: list all the running container
docker exec: execute commands in a running container.

**docker system prune**
- removes unused data of stopped containers, docker networks, and dangling images. 

**Docker Swarm**
Docker Swarm is a tool for managing a group of Docker containers that work together as a single unit, called a "swarm." It allows you to deploy and manage your applications across multiple machines, making them more resilient and scalable.
- a group of Docker hosts into a single and virtual docker host

Here’s how it works in simple terms:

- Clustering: You can combine several Docker hosts (machines) into a single swarm. This lets you run your containers on any machine in the swarm.

- Load Balancing: Docker Swarm automatically distributes incoming traffic among the containers, so they work together efficiently.

- High Availability: If one container fails, Docker Swarm can automatically restart it or move it to another machine in the swarm.

- Simplified Management: You can manage all the containers in the swarm with simple commands, making it easier to deploy and scale your applications.

Overall, Docker Swarm helps you run your applications smoothly across multiple machines while ensuring they stay available and responsive.

**Docker Checkpoint**
The creation of snapshots of a running container’s state , including its file system and the memory. It is useful for experimental mode of scenarios such as debugging or migration.

**Docker Secrets**
Docker secrets are used mostly to securely store sensitive information, such as passwords or API keys in Docker swarm

Docker in production
Prometheus for real-time insights retriving for container performance
Docker states and Docker Events are used to monitoring docker in the production environment.

Explain Implementation method of Continuous Integration(CI) and Continues Development (CD) in Docker?
You need to do the following things:
- Runs Jenkins on docker
- You can run integration tests in Jenkins using docker-compose

A project has a Dockerfile ...
cd to project directory
docker build -t container_name .
docker run -p port contianer_name

or for docker-compose
docker-compose up

Docker Trusted Registry is the enterprise-grade image storage toll for Docker

**Docker-Host:** It contains container, images, and Docker daemon. It offers a complete environment to execute and run your application.
