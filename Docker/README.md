**What is Docker?**

Docker is the client-server type of application which means we have clients who relay to the server. So the Docker daemon called: dockerd is the Docker engine which represents the server, can run on any OS

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
Inside a registry, you can have a repository for each application, and inside each repository you can have multiple images (for each version of the application) => collection of related images
- docker push myorg/img
- docker pull myorg/img


- Docker Compose: helps manage multi-container docker image with docker-compose.yml
  - Services: Each container that your application needs (like a web server, database, etc.).
  - Networks: How the containers communicate with each other.
  - Volumes: Where data is stored and how it's shared between containers.

States of a Docker Container:
- docker ps // shows all running containers
- running, paused (temporarily halted), stopped
- docker start <container_name>
- docker stop <container_name>
- docker kill <container_name>

- sudo docker run -i -t alpine /bin/bash // run image as container

**Hypervisor** is like vmware that allows to run other OS while while docker uses Docker engine

When container is deleted, data is lost => **Docker volumes** to save the data

RUN vs CMD vs ENTRYPOINT
- RUN: Executes commands during the image build process
- CMD: Specifies the default command to run inside the container environment
- ENTRYPOINT: Defines the main command that will always run when the container starts

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

docker run: run the docker image as a docker container.
docker ps: list all the running container
docker exec: execute commands in a running container.

Docker Trusted Registry is the enterprise-grade image storage toll for Docker

**Docker-Host:** It contains container, images, and Docker daemon. It offers a complete environment to execute and run your application.

ARG UBUNTU_VERSION=20.04
ARG: This keyword declares a variable that can be passed to the Docker build process. It’s used for parameters that you might want to change when building the image without modifying the Dockerfile itself.

**ARG vs ENV**
- ARG defines a variable that is only available during the image build process. It cannot be accessed by the running container.
- ENV sets environment variables that are available both during the build process and in the running container.

**Docker Commands**
- :$ docker inspect <repository_name> will provide detailed info of the mentioned image
- :$ docker log <containerID> displays terminal output

**Container Linking**

You must first name the containers before linking
- :$ docker run -it --name container1 -d ubuntu
Now we name container 2 and link it with the named container1
- :$ docker run -it --name container2 --link container1 -d ubuntu

Try this task

- :$ docker run -it --name container1 -d ubuntu
Output = container1_ID
- :$ docker run -it --name container2 --link container1 -d ubuntu
Output = container2_ID

Go inside container2 
- :$ docker exec -ti container2_ID bash
Now we are inside container2
- :$ cat /etc/hosts
Output will give container1's IP addr

Now we will try pinging container1 from container2
- :$ apt-get update
- :$ apt-get install inputils-ping
- :$ ping container1

Essentially, we are establishing a network connection from container2 to container1 so they can communicate. This communication is not possible without linking.

**Docker in the Big Picture of Deployment**

Developer codes JS app files with MongoDB container

- Commits the JS code files in Git
- The Git commit triggers Jenkins which builds the docker image    [CI/CD process initiates]
- The resulting image is pushed into the company/organization's private registry repository
- The deployment server pulls our applications image from private registry's repo and pulls MongoDB image from the public registry - Both our container and MongoDB container will talk with each other based on our Dockerfile configuration

**Top 15 Commands**

Sure! Here are the top 15 commands commonly used in a Dockerfile:

1. **FROM**: Specifies the base image for the Docker image.
2. **RUN**: Executes commands in a new layer on top of the current image and commits the results.
3. **CMD**: Provides defaults for an executing container, specifying the command to run.
4. **ENTRYPOINT**: Configures a container to run as an executable.
5. **COPY**: Copies files and directories from the host filesystem into the image.
6. **ADD**: Similar to COPY, but also supports remote URLs and automatic extraction of compressed files.
7. **ENV**: Sets environment variables in the container.
8. **EXPOSE**: Informs Docker that the container listens on the specified network ports at runtime.
9. **VOLUME**: Creates a mount point with the specified path and marks it as holding externally mounted volumes from native host or other containers.
10. **WORKDIR**: Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions.
11. **USER**: Sets the username or UID to use when running the image.
12. **ARG**: Defines a variable that users can pass at build-time to the Dockerfile with the `docker build` command.
13. **LABEL**: Adds metadata to an image, which can include version, description, and maintainer information.
14. **HEALTHCHECK**: Tells Docker how to test a container to check that it is still working.
15. **SHELL**: Allows the default shell used for the shell form of commands to be overridden.

```dockerfile
FROM ubuntu:20.04

RUN apt-get update && apt-get install -y python3

CMD ["python3", "app.py"]

ENTRYPOINT ["python3", "app.py"]

COPY . /app

ADD http://example.com/file.tar.gz /app/

ENV APP_ENV=production

EXPOSE 80

VOLUME ["/data"]

WORKDIR /app

USER appuser

ARG VERSION=1.0

LABEL maintainer="you@example.com" version="1.0"

HEALTHCHECK CMD curl --fail http://localhost/ || exit 1

SHELL ["powershell", "-Command"]
```
