# Introduction to Jenkins

## 🚀  Introduction to CICD 
Continuous Integration and Continuous Delivery (CI/CD) is a set of best practices and methodologies that revolutionize the software development lifecycle by enhancing efficiency, reliability, and speed. CI/CD represents a seamless integration of automation and collaboration throughout the development process, aiming to deliver high-quality software consistently and rapidly. In the realm of Cl, developers regularly integrate their code changes into a shared repository, triggering automated builds and tests to detect integration issues early. On the other hand, CD encompasses both Continuous Delivery and Continuous Deployment, ensuring that software is always in a deployable state and automating the deployment process for swift and reliable releases. The CI/CD pipeline fosters a culture of continuous improvement, allowing development teams to iterate quickly, reduce manual interventions, and deliver software with confidence.


🚀 **CI/CD** is also a modern software development practice that automates and streamlines the process of building, testing, and deploying code. It stands for:

# 🧱1. Continuous Integration (CI)

**Definition:** CI is the practice of frequently merging code changes from all developers into a shared repository—usually several times a day. Each integration is automatically built and tested.

**Goal:** Catch bugs early, improve code quality, and reduce integration issues.

**Typical CI Steps**

🚀 Developer pushes code to version control (e.g., Git).

🚀 CI server (e.g., Jenkins, GitHub Actions, GitLab CI) runs:

- Build scripts

- Unit tests

- Static code analysis

- Notifications (e.g., Slack, email)

## ✅ Benefits

- Early bug detection

- Faster feedback

- Encourages smaller, incremental changes

# 🚚 2. Continuous Delivery (CD)

**Definition:** CD ensures that code is always in a deployable state. After CI, it automates the release process so you can deploy anytime with a button click.

**Key Point:** You’re not deploying automatically, but you can deploy at any time.

## ✅ Benefits:

- Safer, faster releases

- Shorter release cycles

- Reduced manual work

# 🚀3. Continuous Deployment (also CD)

**Definition:** Takes things further—automatically deploys every change that passes all stages of the pipeline to production.

**Key Difference from Delivery:** No human intervention; production updates happen automatically.

### ✅ Benefits:

- True automation

- Faster time-to-market

- Continuous feedback from real users



# 🧰 What is Jenkins?

Jenkins is an open-source automation server used to implement Continuous Integration (CI) and Continuous Delivery/Deployment (CD) in software development.

## 🔑 Key Features

| **Feature**      | **Description**                                                                                     |
| ---------------- | --------------------------------------------------------------------------------------------------- |
| 🏗️ Automation   | Automates build, test, and deployment processes.                                                    |
| 🔌 Plugins       | Over 1,800 plugins for integration with tools like Git, Docker, Maven, Kubernetes, Slack, AWS, etc. |
| 💡 Extensibility | Highly customizable and scriptable (e.g., with Groovy pipelines).                                   |
| 🌐 Web UI        | User-friendly web interface for managing jobs and monitoring builds.                                |
| 🤖 Agent Support | Supports distributed builds using master-agent architecture.                                        |

# 🧪 What Jenkins Does

1. Builds Code – compiles code automatically when changes are pushed to Git.

2. Runs Tests – triggers unit/integration tests.

3. Reports Results – notifies developers of build or test failures.

4. Deploys Code – can deploy to staging or production environments.

## 🔧 Use Cases

- Automatically testing code after each commit

- Building Docker images

- Deploying web apps to AWS, Azure, or on-prem

- Generating and emailing reports

- Managing infrastructure pipelines with Terraform or Ansible


## ✅ Getting Started With Jenkins 

Now that we have an idea what Jenkins, let's dive into installing Jenkins.

### Update package repositories

``` bash
sudo apt update
```

![](./Images/1.%20sudo-update.png)


- Install JDK

``` bash
sudo apt install default-jdk-headless
```

![](./Images/2.%20install-jdk.png)


- Install Jenkins

``` bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
/etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt-get install jenkins
```

![](./Images/3.%20installing.png)


The command installs Jenkins. It involves importing the Jenkins GPG key for package verification, adding the Jenkins repository to the system's sources, updating package lists, and finally, installing Jenkins through the package manager (apt-get).

Checking if jenkins has been installed, and it is up and running


``` bash
sudo systemctl status jenkins
```

![](./Images/4.%20successfully-installed.png)


On our Jenkins instance, create new inbound rules for port 8080 in security group By default, jenkins listens on port 8080, we need create an inbound rule for this in the security group of our jenkins instance

![](./Images/5.%20port-8080.png)


# Set up Jenkins on the Web Console

1. Input your Jenkins Instance ip address on your web browser and add :8080 to the public Ip address

![](./Images/5.%20jenkins.png)

2. check for password of your instance

![](./Images/7.%20password.png)

3. installed suggested plugins

![](./Images/6.%20customize-jenkins.png)

4. Create account for User

![](./Images/8.%20getting-started.png)

5. Start using jenkins

![](./Images/9.%20start-using-jenkins.png)

6. Login to Jenkins console

![](./Images/10.%20welcome-to-jenkins.png)


# Jenkins Job

## 🛠️ What is a Jenkins Job?

A `Jenkins job` is a task or project that Jenkins runs—like building code, running tests, deploying applications, or automating scripts. Each job defines what to do, when to do it, and how.

## ✅ Types of Jenkins Jobs

| **Type**              | **Description**                                                                 |
|-----------------------|----------------------------------------------------------------------------------|
| Freestyle Project     | Basic, GUI-based jobs—easy to configure for simple tasks.                       |
| Pipeline              | Scripted jobs using Groovy—best for complex workflows (CI/CD).                  |
| Multibranch Pipeline  | Automatically builds pipelines for each branch in a repo.                       |
| Folder                | Used to organize multiple jobs.                                                 |
| Matrix Project        | Run the same job across different environments/parameters.                      |


## ⚙️ Basic Freestyle Job 

1. Create a Freestyle Job

- Go to Jenkins dashboard → New Item

- Name your job → Select Freestyle project → Click OK

2. Configure Job

- Source Code Management: Git (provide repo URL)

- Build Triggers: e.g., poll SCM, build periodically, or on webhook

- Build Steps:

Execute Shell:

``` bash
echo "Building my project"
make build
```
- Post-Build Actions: e.g., email notification, deploy artifact

3. Save & Run

- Click Build Now to run the job manually.

- Or wait for auto trigger based on your settings.


## 🔄 Pipeline Job Example

1. Create a Pipeline Job

- New Item → Choose Pipeline → OK

2. Pipeline Script (Declarative Syntax):

``` bash

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building code...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to production...'
            }
        }
    }
}
```

3. Save and run

## 📦 Common Jenkins Job Use Cases

- Compile Java, Node.js, Python, or C++ code

- Run unit/integration tests

- Package Docker containers

- Deploy to Kubernetes or AWS

- Send status emails or Slack alerts

- Lint or check code style


## 🧠 Jenkins Job Best Practices

- Use Pipelines for anything beyond simple builds.

- Keep builds reproducible and isolated (e.g., Docker agents).

- Use credentials plugins to protect secrets.

- Store pipeline scripts in Git (Jenkinsfile) for version control.


## Creating a Freestyle Project

- Let's create our first build job

From the dashboard menu on the left side, click on new item

![](./Images/11.%20new-item.png)


- Create a freestyle project and name it cassieWebapp

![](./Images/12.%20new-item.png)

- give it a description

![](./Images/13.%20general.png)

![](./Images/13b.%20general.png)


- note always Apply before you save 

![](./Images/13c.%20general.png)


- successful jenkins freestyle project

![](./Images/14.%20success.png)



**Connecting Jenkins To Our Source Code Management**

Lets connect jenkins with github

- Create a new github repository called `jenkins-scm with README.md file

![](./Images/15.%20new-repo.png)

- Connect jenkins to jenkins-scm repository by pasting the repository url.

![](./Images/16.%20git-connect-to-jenkins.png)

![](./Images/17.%20first-job.png)

![](./Images/18.%20triggers.png)

![](./Images/19.%20git-setting.png)

![](./Images/20.%20jenkins-url.png)

![](./Images/21.%20push.png)


## Jenkins Pipeline Job

A Jenkins Pipeline job is a specialized job in Jenkins that defines a series of automated steps (called a pipeline) to build, test, and deploy code. It’s written as code using the Pipeline DSL (Domain Specific Language), typically in a file called Jenkinsfile.

## What is a Jenkins Pipeline Job

A Jenkins pipeline job is a way to define and automate a series of steps in the software delivery process. It allows to script and organize the entire build, test, and deployment. Jenkins pipelines enables organizations to define, visualize, and execute intricate build, test, and deployment processes as code. This facilitates the seamless integration of continuous integration and continuous delivery (CI/CD) practices into software development.

I'm going to use the dockerfile image I created in the docker foundation project in this project.

## Creating a Pipeline Job

1. Back to the Jenkins dashboard, on the menu on the left side, click on New Item. `1. New Item`
2. Then I name this pipeline My pipeline job and select Pipeline under item type. `2. Pipeline Job`
3. Then on the left side click on Triggers then tick the box for GitHub hook trigger for GITScm polling? and save it. `3. Trigger` 

Since I have created a GitHub webhook previously in my last project I don't need to create another one again.

## Writing Jenkins Pipeline Script

A jenkins pipeline script refers to a script that defines and orchestrates the steps and stages of a continuous integration and continuous delivery (CI/CD) pipeline. Jenkins pipelines can be defined using either declarative or scripted language to describe the pipeline stages, steps, and other configurations while scripted syntax provides more flexiblity and is suitable for complex scripting requirements.

Here's my pipeline script

``` bash
pipeline {
    agent any
    stages {
        stage('Connect To GitHub') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Orisuniyanu/jenkins-scm.git'
                    ]]
                ])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t dockerfile .'
                }
            }
        }
        stage('Run Docker Container') { 
            steps {
                script {
                    sh 'docker run -itd -p 8081:80 dockerfile'
                }
            }
        }
    }
}
```

## Explanation of the Script Above

The provided Jenkins pipeline script defines series of stage for a continuous integration and continuous delivery (CI/CD) process. Let's breakdown each stage:

- **Agent Configuration:**

``` bash
agent any
```

Specifies that the pipeline can run on any available agent (an agent can either be a Jenkins master or node). This means the pipeline is not tied to a specific node type.

- **Stages:**

``` bash
stages {"\n      // Stages go here\n   "}
```

Defines the various stages of pipeline, each representing a phase in the software delivery process.

- **Stage 1: Connect To GitHub:**

``` bash
stage('Connect To Github') {"\n      steps {\n         checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/RidwanAz/jenkins-scm.git']])\n      "}
}
```

- This stage checks out the source code from a GitHub repository [`https://github.com/Orisuniyanu/jenkins-scm.git](https://github.com/Orisuniyanu/jenkins-scm).

- It specifies that the pipeline should use the 'main' branch.

- **Stage 2: Build Docker Image:**

``` bash
stage('Build Docker Image') {"\n      steps {\n         script {\n            sh 'docker build -t dockerfile .'\n         "}
   }
}
```

- This stage builds a docker image named 'dockerfile' using the source code obtained from the Github repository.

The **docker build** command is executed using the shell (**sh**).

**Stage 3: Run Docker Container:**

``` bash
stage('Run Docker Container') {"\n      steps {\n         script {\n            sh 'docker run -itd --name nginx -p 8081:80 dockerfile'\n         "}
   }
}
```

- This stage runs Docker container names 'nginx' in detached mode (**-itd**).
- The container is mapped to port 8081 on the host machine (**-p 8081:80**).
- The Docker image used is the one built in the previous stage ('dockerfile').

4. After written the pipeline script then I copied it and paste it under Pipeline script, then click on Pipeline Syntax. 4. Pipeline Syntax

5. After that another tab was opened, then under Sample Step I select checkout: Check out from version control. 5. Generator

6. Then I paste my GitHub URL to the provided space and change the branch from master to main. 6. Pipeline Syntax

7. Then click on Generate Pipeline Script 7. Generate Pipeline Script

8. Then I copied the generated syntax and paste and replace the checkout stage. 8. CheckOut

### Installing Docker

Before Jenkins can run docker commands, we need to install docker on the same instance Jenkins was installed. I will be installing the docker with a shell script to demostarte my knowledge in shell scripting.

1. Open my EC2 instance through putty application. 9. Putty

2. Then I create a new file which I name docker.sh with vim text editor the paste the below commands and save it with :wq!. 10. VIM


## Explaination of the command inside the script

1. Update package index

``` bash
sudo apt-get update -y
```

- sudo: Runs the command with administrator (root) privileges.

- apt-get update: Updates the list of available packages and their versions from all configured sources.

- -y: Automatically says "yes" to any prompts.

2. Install required dependencies

``` bash
sudo apt-get install ca-certificates curl gnupg
```

- ca-certificates: Contains root certificates to authenticate SSL connections.

- curl: A command-line tool to fetch data from URLs (like downloading files).

- gnupg: Used for encryption and signing data (here, it helps verify Docker's authenticity).

3. Create a directory for Docker’s GPG key

``` bash
sudo install -m 0755 -d /etc/apt/keyrings
```

- install: Not just for copying files; also used to create directories with specific permissions.

- -m 0755: Sets the permissions (owner can read/write/execute; others can read/execute).

- -d: Create a directory.

- /etc/apt/keyrings: A secure location for storing third-party GPG keys.

4. Download Docker’s GPG key and save it

``` bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

- curl -fsSL: Downloads the file quietly and fails silently on errors.

- |: Pipes the output to the next command.

- gpg --dearmor: Converts the key from ASCII-armored format to binary.

- -o: Specifies the output file.

5. Set permissions for the Docker GPG key

``` bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

- chmod a+r: Gives all users (a) read (r) access to the key file.

6. Add Docker's official repository

``` bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- dpkg --print-architecture: Gets your system’s architecture (e.g., amd64).

- /etc/os-release and $VERSION_CODENAME: Detects your Ubuntu version codename (e.g., jammy, focal).

- signed-by=...: Ensures the repository uses the specified trusted GPG key.

- tee: Writes the output to the Docker repository file.

- /dev/null: Prevents output from being shown on screen.

7. Update package index again

``` bash
sudo apt-get update -y
```

- Necessary to include the new Docker repo in the package index.

8. Install Docker Engine and components

``` bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

- docker-ce: Community Edition of Docker.

- docker-ce-cli: Docker command-line interface.

- containerd.io: Container runtime used by Docker.

- docker-buildx-plugin: Enhances Docker's build command with more features.

- docker-compose-plugin: Enables use of docker compose command.

- -y: Confirms installation automatically.

9. Check Docker service status

``` bash
sudo systemctl status docker
```

10 systemctl status: Shows if Docker is running and its overall health.

- Then I make the file executable by adding x permission for user which is basically me.

``` bash
chmod u+x docker.sh
```

11. Then I execute the file

``` bash
./docker.sh
```

`11. Install Docker` And docker is installed and running `12. Docker Running`

12. Then I create another file for docker file which is named Dockerfile then paste the following syntax inside the file.

``` bash
vim Dockerfile

# Use the official NGINX base image
FROM nginx:latest

# Set the working directory in the container
WORKDIR  /usr/share/nginx/html/

# Copy the local HTML file to the NGINX default public directory
COPY index.html /usr/share/nginx/html/

# Expose port 80 to allow external access
EXPOSE 80
```

13. Also I create another file which is index.html and paste the following in it.

``` bash
vim indec.hml

Congratulations, You have successfully run your first pipeline code.
```

`13. Dockerfile` 7. Then I push the 2 files to my remote repository.

``` bash
git init
git add .
git remote add origin https://github.com/Orisuniyanu/jenkins-scm.git
git remote -v
git pull origin main --allow-unrelated-histories
git pull origin main --rebase
git push -u origin main
```

`14. Git Push`

14. Then went back to the Jenkins and check it was ran successfully. `15. Console Output`

15. Then open my AWS account and go to the EC2 instance dashboard and click on `Security group` under Network & Securuty, then click on Edit inbound rule. `16. Security Group`

16. Then click on `Add rule` then allow port 8081 which is the port our docker container is running on, then click on Save rule. `17. Inbound Rule`

17. After that I copied my public Ip address then open my browser and type this URL `http://54.153.82.`196:8081/ `18. Website` This show my project is successful executed.

