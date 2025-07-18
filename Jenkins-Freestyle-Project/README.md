# Jenkins Freestyle Project

## Jenkins Job

## 🛠️ What is a Jenkins Job?

A Jenkins job is a task or project that Jenkins runs—like building code, running tests, deploying applications, or automating scripts. Each job defines what to do, when to do it, and how.


## ✅ Types of Jenkins Jobs


| **Type**              | **Description**                                                                 |
|-----------------------|----------------------------------------------------------------------------------|
| Freestyle Project     | Basic, GUI-based jobs—easy to configure for simple tasks.                       |
| Pipeline              | Scripted jobs using Groovy—best for complex workflows (CI/CD).                  |
| Multibranch Pipeline  | Automatically builds pipelines for each branch in a repo.                       |
| Folder                | Used to organize multiple jobs.                                                 |
| Matrix Project        | Run the same job across different environments/parameters.                      |


## ⚙️ Basic Freestyle Job Example

1. Create a Freestyle Job

- Go to Jenkins dashboard → New Item

- Name your job → Select Freestyle project → Click OK

2. Configure Job

- Source Code Management: Git (provide repo URL)

- Build Triggers: e.g., poll SCM, build periodically, or on webhook

- Build Steps:


📦  Executive Shell:

``` bash
echo "Building my project"
make build
```

- Post-Build Actions: e.g., email notification, deploy artifact

3. Save & Apply

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

3. Save & Apply



# 📦 Common Jenkins Job Use Cases

- Compile Java, Node.js, Python, or C++ code

- Run unit/integration tests

- Package Docker containers

- Deploy to Kubernetes or AWS

- Send status emails or Slack alerts

- Lint or check code style


# 🧠 Jenkins Job Best Practices

- Use Pipelines for anything beyond simple builds.

- Keep builds reproducible and isolated (e.g., Docker agents).

- Use credentials plugins to protect secrets.

- Store pipeline scripts in Git (Jenkinsfile) for version control.


## Creating a Freestyle Project

- Let's create our first build job

    - From the dashboard menu on the left side, click on new item

- From the dashboard menu on the left side, click on new item

![](./Images/1.%20jenkins.png)


- Create a freestyle project and name it `my-first-job` 

![](./Images/2.%20freestyle.png)


### Connecting Jenkins To Our Source Code Management

- Lets connect jenkins with github

Create a new github repository called `jenkins-scm with README.md file`

![](./Images/3.%20new-repo.png)

- scroll down to branch specific and change it from `master` to `m`ain` or what ever your actual branch name is on github

![](./Images/4b.%20branch-specific.png)


Connect `jenkins` to `jenkins-scm` repository by pasting the repository url.

![](./Images/5.%20success.png)


# Configure Build Trigger

As an engineer we need to be able to automate things and make our work easier in possible ways. We have connected `Jnkins` to our `Jenkins-scm` but we can not a new build by clicking on **Build Now**. To eliminate this, we need to configure a build trigger to our Jenkins job. With this, Jenkins will run a new build anytime a change is made to our github repository.

- Click `configure` and 
- click `trigger` 
- create a github webhook using jenkins ip address and port

![](./Images/6.%20webhook.png)

- successfully pushed to git hub

![](./Images/7.%20pushed.png)  

![](./Images/8.%20success.png)







