# Working with Docker Container

## Introduction to Docker Container

Docker containers are lightweight, portable, and executable units that encapsulate an application and its dependencies.

## ✅ What Are Containers?

A container is a standalone executable package that includes:

- The application code

- Runtime environment

- System tools and libraries

- Configuration files

This allows the application to run reliably regardless of where it is deployed — on a developer's laptop, on-premises servers, or in the cloud.

## ✅ Why Use Docker Containers?

1. Portability

- Containers can run on any system that supports Docker, eliminating the "it works on my machine" problem.

2. Isolation

- Each container runs in its own environment, separate from other containers or the host system.

3. Resource Efficiency

- Containers share the host OS kernel, making them lighter and faster than virtual machines (VMs).

4. Scalability

- Docker works well with orchestration tools (like Kubernetes), making it easy to scale applications.

5. Version Control & Reusability

- Docker images can be versioned and reused across projects or teams.


## ✅ Running Containers

To run a container, you use the `docker run` command followed by the name of the image you want to use. The command launches a container based on ubuntu image.

``` bash
docker run ubuntu
``` 

![](./Images/1.%20docker-run.png)


The image above shows that the container is created but not running. we can start the container by running. 

``` bash
docker start CONTAINER_ID
```

![](./Images/2.%20container-ID.png)


## Launching Containers with Different Options

Docker provides various options to customize the behaviour of containers. For example, you can specify environment variables, map ports, and mont volumes.

Here's an example of running a container with a specific environment variable:

``` bash
docker run -e "MY_VARIABLE=my-value" ubuntu
```

![](./Images/12.%20docker-variable.png)


### Running container in the Background

By default, containers run in the foreground, and the terminal is attached to the container's standard input/output. To run a container in the background use the `-d` flag

``` bash
docker run -d ubuntu
```
![](./Images/3.%20-d-flage.png)

This command starts a container in the background, allowing you to continue the terminal.


## Container Lifecycle

Containers have a lifecycle that includes creating, starting, stopping, and restarting. Once a container is created, it can be started and stopped multiple times.

**Starting, Stopping, and Restarting Containers**

- showing start container

![](./Images/4.%20docker-stoped.png)


- To start a stopped container:

``` bash
docker start container_name
```
- docker start cool_burnell

![](./Images/6.%20ec2-docker-start.png)


- To stop a running container

``` bash
docker stop container_name
```

- docker stop cool_burneel

![](./Images/5.%20ec2-docker-stop.png)


## Ubuntu terminal

- View of a stopped container

![](./Images/7.%20ubuntu-ps.png)

- To start a stopped conatiner

![](./Images/8.%20ubuntu-start.png)

- To stop a running container

![](./Images/9.%20ubuntu-stop.png)

- To restart a stopped container

``` bash
docker restart container_name
```

![](./Images/10.%20docker-restart.png)


### Removing Containers

To remove a container, you use the `docker rm` command followed by the container's ID or name:

``` bash
docker rm container_name
```

![](./Images/11.%20docker-rm.png)

This deletes the container, but keep in mind that the associated image remains on your system.








