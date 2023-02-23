## CONTINUOUS DELIVERY ON AWS


**Because in an Agile SDLC, there will be frequent code changes**


- Manual code deployment is time consuming

- The Ops team won't be able to cope with such delivery

- There is also lot of dependencies here

- The developer will be dependent of build and release team

- Those team will be dependent on OPs team, build and release team

- Interaction will be happening via ticketing system, emails or other tools

- There are many tools involved which delays the process of SDLC



### SOLUTION

**Continuous delivery**


#### Build - Test - Deploy - and test for every commit

**How can it help you?**

- It is an Automated process

- You can be notified for every build status

- Fix code if bugs or error is found instantly instead of waiting



#### WORKFLOW


- Developers will make changes to the code and push to github which also have our Jenkins pipeline code

- Code will be fetched from Github by Jenkins, and using Maven, we will run a unit test.

- Checkstyle will perform code analysis

- Sonar scanner will again run code analysis and the result will be uploaded to sonarqube server, check the quality gate and if everything is good, we proceed to next stage

- Build the docker image which will have the java artifact in it. 

- The docker image will be a Tomcat docker image with our artifact in that, which will be pushed to Amazon ECR

- Then we will use AWS CLI command from jenkins pipeline which will deploy the latest image to ECS cluster.

- So basically  Amazon ECS will fetch the latest image from Amazon ECR and run it in the ECS cluster


### Objective

- Fault Isolation

- Short MTTR

- Fast turn around time: if there is any new request or any code change, it can be implemented quickly

- Less disruptive


### FLOW OF EXECUTION

1. Update github webhook with new jenkins IP

2. Copy Docker files from vprofile repo to our repo

3. Prepare 2 separate jenkins file for staging and production in source code

4. AWS steps

a. IAM, ECR repo setup


5. Jenkins step

**installing following plugins**

- Amazon ECR

- Docker, docker build and publish

- Pipeline: aws steps


6. Install docker engine & awscli on jenkins

7. Write Jenkinsfile for build and publish image to ECR

8. ECS setup

   - cluster, task definition, service

9. Write code for deploy docker image to ECS

10. Repeat the steps for prod ECS cluster

11. Promoting docker image for production

