# Introduction to Docker and Containers

## What is Docker
Docker is a platform for developing, shipping, and running applications using containerization. Containers allow you to package up an application along with everything it needs to run (code, libraries, dependencies, etc.) so that it runs consistently across different environments.

## 🔹Key Concepts:

1. ### Container

- lightweight, standalone, executable package.
- Contains everything needed to run a piece of software.
- Think of it as a mini virtual machine, but more efficient and faster.

2. ### Image

- A snapshot or blueprint used to create containers.
- You build an image using a file called a **Dockerfile**.
- Once built, images can be run as containers.

3. ### Dockerfile

- A script with instructions for building a Docker image.

✅ Example

``` bash
FROM python:3.10
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

4. ### Docker Hub

- A public repository for sharing Docker images.
- You can pull prebuilt images (e.g., nginx, mysql) or push your own.

5. ### Docker Engine

- The core part of Docker that runs and manages containers.

## 🔹 Why Use Docker?

📌 **Portability:** Runs the same on a developer's laptop and in production.

📌 **Isolation:** Each container is isolated, preventing conflicts.

📌 **Scalability:** Easily scale up/down with container orchestration tools like Kubernetes.

📌 **Efficiency:** Uses fewer resources than full virtual machines.


# 🧱 Docker Containers vs Virtual Machines

| Feature         | Docker Containers                                           | Virtual Machines                                    |
|----------------|-------------------------------------------------------------|-----------------------------------------------------|
| Architecture    | Shares the host OS kernel                                   | Runs full OS with a separate kernel                 |
| Startup Time    | Seconds                                                     | Minutes                                             |
| Size            | Lightweight (MBs)                                           | Heavy (GBs)                                         |
| Isolation       | Process-level isolation                                     | Full machine-level isolation                        |
| Performance     | Near-native speed                                           | Slightly slower due to hypervisor overhead         |
| Portability     | Highly portable across environments                         | Portable, but less flexible                         |
| Resource Usage  | Uses fewer CPU/memory resources                             | Requires more resources                             |
| Use Case        | Microservices, CI/CD, DevOps, cloud-native apps             | Full OS simulation, legacy apps, strong isolation   |
| Security        | Good (shares kernel, slightly more risk)                    | Strong (full isolation)                             |


## 🖼️ Visual Summary 

### 🚀 Virtual Machine Stack:

``` bash
Hardware
  └── Host OS
      └── Hypervisor
          ├── Guest OS 1
          └── Guest OS 2          
```

## 🚀 Docker Stack:

``` bash
Hardware
  └── Host OS
      └── Docker Engine
          ├── Container 1
          └── Container 2
```


## ✅ When To Use Which:

| Scenario                                      | Best Option |
|----------------------------------------------|-------------|
| Rapid deployment, microservices, CI/CD       | Docker      |
| Strong isolation, running multiple OS types  | VM          |
| Resource-constrained environment             | Docker      |
| Running full Windows inside Linux (or vice versa) | VM     |


# Getting Started with Docker

### Installing Docker

**first, let add Docker's officail GPG Key**
click [here](https://help.ubuntu.com/community/GnuPrivacyGuardHowto)

1. Launch an Ubuntu 24.04.1 LTS
![](./Images/1.%20launch-Ubuntu.png)


``` bash
sudo apt-get update
```

- The above linux command refreshes the package list on a Debian-based system, ensuring the latest software information is available for installation.

![](./Images/2.%20Update.png)


``` bash
sudo apt-get install ca-certificates curl gnupg
```
- The above Linux command installs essential packages including certificate authorities, a data transfer tool (curl) and the GUN privacy Guard for secure communication and package verification.

![](./Images/3.%20gpg.png)


``` bash
sudo install -m 0755 -d /etc/apt/keyrings
```

- The command above create a directory (/etc/apt/keyrings) with specific permissions (0755) for storing keyring files, which are used for docker's authentications.


![](./Images/4.%20docker-file.png)

``` bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

- The above command downloads the Docker GPG key using 'curl'

![](./Images/5.%20curl-fssl.png)


``` bash 
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

- This sets read permissions for all users on the Docker GPG key file within the APT kingring directory.

![](./Images/6.%20set-permissions.png)


## 2.  Add the repository to Apt sources

``` bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
``` 

- The `echo` command creates a Docker APT repository configuration entry for the Ubuntu system, incorporating the system architecture and Docker GPG key, and the sudo tee /etc/apt/sources.list.d/docker.list > /dev/null writes this configuration to /etc/apt/sources.list.d/docker.list file

![](./Images/7.%20echo.png)


- Refresh the package list

![](./Images/8.%20sudo-update.png)


- Install latest version of Docker

``` bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

![](./Images/9.%20install-docker.png)

- Verify that Docker has been successfully installed

``` bash
sudo systemctl status docker
```

![](./Images/10.%20docker-running.png)


- By default, after installing docker, it can only be run by root user or using sudo command. To run the docker command without sudo execute the command below

``` bash
sudo usermod -aG docker ubuntu
```

my root user is sandraolis not ubuntu

![](./Images/11.%20usermod.png)

After executing the command above, we can run Docker command without using superuser privileges. 



## Run the "Hello-World" Container

Using the `docker run` command

The `docker run` command is the entry point to execute containers in Docker. It allows you to create and start a container based on a specified Docker image. The most straightforward example is the "Hello World" container, a minimalistic container that prints a greeting message when executed.

``` bash
# Run the "Hello World" container
docker run hello-world
```

![](./Images/12.%20hello-world.png)


When you execute this command, Docker performs the following steps:

1. **Pulls image (if not available locally)**: Docker checks if the `hello-world` image is available locally. If not, it automatically pulls it from the Docker Hub, a centralized repository for Docker images.

2. **Creates a Container**: Docker creates a container based on the `hello-world` image. This container is an instance image, with its own isolated filesystem and runtime environment.

3. **Starts the Container**: The container is started, and it executes the predefined command in the hello-world image, which prints a friendly message.


## Understanding the Docker Image and Container Lifecycle

**Docker Image**: A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries and system tools. Images are immutable, meaning they cannot be modified once created. Changes result in the creation of a new image.

**Container Lifecycle**: Containers are running instances of Docker images.
They have a lifecycle: `create`, `start`, `stop`, and `delete`.

Once a container is created from an image, it can be `started`, `stopped` and `restarted`.



## Verifyig the Successful Execution

You can check if the images is now in your local environment with Example Output:

``` bash
docker images
```


![](./Images/13.%20docker-images.png)

If you encounter any issues, ensure that Docker is properly installed and that your user has the necessary permissions to run Docker commands.

This simple `Hello-World` example serves as a basic introduction to running containers with Docker. It help verify that your Docker environment is set up correctly and provides insight into the image and container lifecycle. 


## Basic Docker Commands

- **Docker Run**

The `docker run` command is fundamental for executing containers. It creates and starts a container based on a specified image.

``` bash
# Run a container based on the "nginx" image
docker run nginx
```

![](./Images/14.%20docker-nginx.png)

This example pulls the nginx image from Docker Hub (if not available locally) and starts a container using that image.

- ### Docker ps

The `docker ps` command displays a list of running containers. This is useful for monitoring active containers and obtaining information sucha as container IDs, names, and status.

``` bash
# List running containers
docker ps
```

To view all containers, including those that have stopped, add the -a option

``` bash
# List all containers (running and stopped)
docker ps -a
```

![](./Images/16.%20docker-ps.png)


- ### Docker Stop

The docker stop command halts a running container.

``` bash
# Stop a running container (replace CONTAINER_ID with the actual container ID)
docker stop CONTAINER_ID
```

![](./Images/17.%20docker-stop.png)


- ### Docker pull

The `docker pull` command downloads a Docker image from a registry, such as Docker Hub, to your local machine.

``` bash
# Pull the latest version of the "ubuntu" image from Docker Hub
docker pull ubuntu
```


![](./Images/18.%20docker-pull.png)

For you to be able to push your images to Docker hub, you need to login to your docker hub account. After loggin successfully then you push.

![](./Images/19.%20docker-login.png)


- ### Docker Push

The `docker push` command uploads a local Docker image to a registry, making it available for others to pull.

``` bash
# Push a local image to Docker Hub
docker push your-username/image-name
```

![](./Images/20.%20docker-tag-push.png)


Image successfully pushed to my Docker hub

![](./Images/21.%20docker-hub.png)


- ### Docker images

The `docker images` command lists all locally available docker images

``` bash
# List all local Docker images
docker images
```

![](./Images/22.%20docker-images.png)


- ### Docker RMI

The `docker rmi` command removes one or more images from the local machine.

``` bash
# Remove a Docker image (replace IMAGE_ID with the actual image ID)
docker rmi IMAGE_ID
```

![](./Images/23.%20rempve-id-container.png)

These basic Docker commands provide a foundation for working with containers. Understanding how to run, list, stop, pull, push and manage Docker images is crucial for effective containerization and orchestration. As you delve deeper into Docker, you'll discover additional commands and features that enhance your ability to develop, deploy, and maintain containerized applications.













