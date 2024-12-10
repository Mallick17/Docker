# Docker
Commands and Installation and Study Notes
### Installation of Docker Commands
# Docker & Docker-Compose Setup on Linux
  ```sh
  sudo yum update -y
  sudo yum search docker
  sudo yum info docker
  sudo yum install -y docker
  sudo systemctl enable docker.service
  sudo systemctl start docker.service
  sudo systemctl status docker.service
  docker --version
  sudo yum install git -y
  sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  docker-compose --version
  ```
  ## Task-1
<details>
<summary><strong>Pull an httpd image, run a container, stop the container, restart it, and remove the Docker image</strong></summary>
<br>

```bash
docker images                ## Lists available images on the system; used to check image availability.
docker ps                    ## Shows running containers; used to monitor active containers.  
docker pull httpd            ## Downloads the httpd image from Docker Hub; used to prepare an image.
docker images                ## Verifies the httpd image is downloaded.
docker run -it -d httpd      ## Starts an httpd container in detached interactive mode; used to deploy containers. 
docker ps                    ## Verifies the httpd container is running.
docker stop container_id     ## Stops the running container; used to halt container processes.
docker ps -a                 ## Lists all containers, including stopped ones.
docker start container_id    ## Restarts the stopped container; used to resume operations.
docker stop container_id     ## Stops the restarted container.
docker rm container_id       ## Removes the stopped container; used to free resources.
docker ps -a                 ## Verifies the container is removed.
docker images                ## Lists all images to confirm existence of the httpd image.
docker rmi httpd             ## Deletes the httpd image; used to clean up unused images.
docker images                ## Confirms the image is removed.
```
</details>

  ## Task-2
<details>
<summary><strong>Pull an httpd image, run a container named 'webapp', stop it, and delete it</strong></summary>
<br>

```bash
docker images                     ## Lists available images on the system; used to check image availability.
docker ps                         ## Shows running containers; used to monitor active containers.
docker pull httpd                 ## Downloads the httpd image from Docker Hub; used to prepare an image.
docker images                     ## Verifies the httpd image is downloaded.
docker run -it -d --name webapp httpd  ## Starts an httpd container in detached mode with the name 'webapp'.
docker ps                         ## Verifies the 'webapp' container is running.
docker stop webapp                ## Stops the running 'webapp' container; used to halt container processes.
docker ps -a                      ## Lists all containers, including stopped ones.
docker rm webapp                  ## Removes the stopped 'webapp' container; used to free resources.
docker ps -a                      ## Verifies the container is removed.
docker images                     ## Lists all images to confirm existence of the httpd image.
docker rmi httpd                  ## Deletes the httpd image; used to clean up unused images.
docker images                     ## Confirms the image is removed.
```
</details>

  ## Task-3
<details>
<summary><strong>Pull an Nginx image, run a container on port 8000, and manage it</strong></summary>
<br>

```bash
docker images                           ## Lists available images on the system; used to check image availability.
docker ps                               ## Shows running containers; used to monitor active containers.
docker pull nginx                       ## Downloads the nginx image from Docker Hub; used to prepare an image.
docker images                           ## Verifies the nginx image is downloaded.
docker run -it -d -p 8000:80 nginx      ## Starts an Nginx container in detached mode with port 8000 mapped to container's port 80.
docker ps                               ## Verifies the Nginx container is running and port 8000 is mapped.
docker stop container_id                ## Stops the running Nginx container; used to halt container processes.
docker ps -a                            ## Lists all containers, including stopped ones.
docker rm container_id                  ## Removes the stopped Nginx container; used to free resources.
docker ps -a                            ## Verifies the container is removed.
docker images                           ## Lists all images to confirm existence of the nginx image.
docker rmi nginx                        ## Deletes the nginx image; used to clean up unused images.
docker images                           ## Confirms the image is removed.
```
</details>

  ## Task-4
<details>
<summary><strong>Pull one nginx image and run a container & take a backup(snapshot) of running container & create a docker image, push into docker hub repository</strong></summary>
<br>

```bash
# Step 1: Check running containers
docker ps                           ## Lists all running containers.

# Step 2: Pull the nginx image
docker pull nginx                   ## Pulls the nginx image from Docker Hub.

# Step 3: Run the nginx container
docker run -it -d nginx             ## Starts an nginx container in detached mode.

# Step 4: Commit the running container to a new image
docker commit b5ef90ae5e8c mallick17/samplenginx    ## Creates a new image 'mallick17/samplenginx' from the container.

# Step 5: Check available images
docker images                       ## Verifies the new image is created.

# Step 6: Log in to Docker Hub
docker login                        ## Logs in to Docker Hub (needed to push images).

# Step 7: Push the new image to Docker Hub before pushing the image, Create dockerhub repo
docker push mallick17/samplenginx                ## Pushes the 'samplenginx' image to Docker Hub.
docker push mallick17/samplenginx:tagname        ## Pushes a tagged version of the image.

# Step 8: Verify running containers
docker ps                           ## Checks currently running containers.

# Step 9: Remove the running container forcefully
docker rm -f b5ef90ae5e8c           ## Deletes the container 'b5ef90ae5e8c'.

# Step 10: Remove the nginx image
docker rmi nginx                    ## Removes the nginx image if unused.
docker rmi -f nginx                 ## Force-removes the nginx image.

# Step 11: Remove the custom image locally
docker rmi mallick17/samplenginx    ## Removes the custom image from the local system.

# Step 12: Pull the custom image back from Docker Hub
docker pull mallick17/samplenginx   ## Retrieves the 'samplenginx' image from Docker Hub.

# Step 13: Log out from Docker Hub
docker logout                       ## Logs out from Docker Hub.
```
</details>

  ## Task-5
<details>
<summary><strong>Pull one amazon Linux image and run the container with the name called webapp & install tomcat & start the tomcat service.</strong></summary>
<br>

```bash
# Step 1: Pull the Amazon Linux image
docker pull amazonlinux                      ## Downloads the Amazon Linux image from Docker Hub.

# Step 2: Verify available images
docker images                                ## Lists the available Docker images.

# Step 3: Run the container in detached mode with the name 'webapp'
docker run -it -d --name webapp amazonlinux  ## Starts the container 'webapp' in detached mode.

# Step 4: Verify running containers
docker ps                                    ## Lists running containers, confirms 'webapp' is active.

# Step 5: Access the running container's shell
docker exec -it 6a075d027f6f /bin/bash        ## Opens a bash shell inside the running 'webapp' container.

# Step 6: Install wget inside the container
yum install wget -y                          ## Installs wget to download files inside the container.

# Step 7: Download Tomcat from Apache servers
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.97/bin/apache-tomcat-9.0.97.tar.gz   ## Downloads the Tomcat tarball.

# Step 8: Install tar to extract the Tomcat archive
yum install tar -y                           ## Installs tar utility to extract Tomcat tarball.

# Step 9: Install gzip to handle compressed files (if not installed)
yum install gzip -y                          ## Installs gzip to handle compressed archives.

# Step 10: Extract the Tomcat archive
tar -zxvf apache-tomcat-9.0.97.tar.gz        ## Extracts the Tomcat tarball.

# Step 11: Verify extracted files
ls                                          ## Verifies that the files have been extracted.

# Step 12: Navigate into the Tomcat directory
cd apache-tomcat-9.0.97                     ## Changes directory to the extracted Tomcat folder.

# Step 13: Verify contents of the Tomcat folder
ls                                          ## Lists contents of the Tomcat directory.

# Step 14: Navigate to the bin directory
cd bin/                                     ## Changes directory to Tomcat's bin folder.

# Step 15: Verify contents in the bin directory
ls                                          ## Lists contents of the bin directory.

# Step 16: Install Java 11 (required by Tomcat)
yum install java-11* -y                      ## Installs Java 11, required for running Tomcat.

# Step 17: Start Tomcat service
sh startup.sh                               ## Starts the Tomcat server using the startup script.

# Step 18: Exit the container shell
exit                                        ## Exits the container shell.

# Step 19: Verify running containers
docker ps                                    ## Verifies the container 'webapp' is still running.
```
</details>
  
# Docker-File
**Dockerfile is a special text file which contains software configuration to build docker images(to build customized docker image).**
- **Dockerfile contains configuration commands like:**
  ```
  yum install wget -y
  wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz
  yum install tar -y 
  yum install gzip -y
  tar -zxvf apache-tomcat-9.0.91.tar.gz
  yum install java-11* -y
  sh /apache-tomcat-9.0.91/bin/startup.sh
  ```
  
<details>
<summary><strong>Hands On Docker-File</strong></summary>
<br>
  
- **Create a `Dockerfile`**
```sh
vi Dockerfile
```
- **Dockerfile Content**
```sh
# Step 1: Use the Amazon Linux base image
FROM amazonlinux

# Step 2: Define the maintainer information
MAINTAINER "gyanaranjanmallick444@gmail.com"

# Step 3: Install necessary dependencies
RUN yum install wget -y                  ## Install wget to download files
RUN wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz  ## Download Tomcat
RUN yum install tar -y                   ## Install tar to extract the Tomcat archive
RUN yum install gzip -y                  ## Install gzip for handling compressed files

# Step 4: Extract the Tomcat archive
RUN tar -zxvf apache-tomcat-9.0.91.tar.gz ## Extract Tomcat

# Step 5: Install Java 11 (required by Tomcat)
RUN yum install java-11* -y              ## Install Java 11

# Step 6: Start Tomcat server
RUN sh /apache-tomcat-9.0.91/bin/startup.sh ## Start Tomcat when the container is built
```
- **Build and Run the Docker Container**
```
# Step 1: Build the Docker image from the Dockerfile
docker build -t tomcat-amazonlinux .      ## Builds the image with the tag 'tomcat-amazonlinux'

# Step 2: Verify the available Docker images
docker images                            ## Lists all available Docker images.

# Step 3: Run the container in detached mode
docker run -it -d --name webapp tomcat-amazonlinux  ## Runs the container in detached mode with the name 'webapp'

# Step 4: List running containers
docker ps                                ## Shows all running containers.

# Step 5: Access the running container shell
docker exec -it <container_id> /bin/bash  ## Access the container shell using the container ID.

# Step 6: Navigate to the Tomcat bin directory
cd /apache-tomcat-9.0.91/bin/             ## Navigate to the Tomcat bin directory.

# Step 7: Start the Tomcat service
sh startup.sh                            ## Starts the Tomcat service.

# Step 8: Exit the container shell
exit                                     ## Exits the container shell.

# Step 9: Verify available Docker images again
docker images                            ## Lists the images to verify the new image.

# Step 10: Remove the container forcefully
docker rm -f <container_id>              ## Force removes the container by ID.

# Step 11: Remove the Docker image
docker rmi tomcat-amazonlinux             ## Removes the 'tomcat-amazonlinux' image.
```
</details>



# Docker-Compose
  ## Task-1
  
# Docker Volume on Linux
  ## Task-1
  
# Docker Swarm Setup on Linux
  ## Steps

  | **Docker-Master**                    | **Docker-Worker**                        |
  |--------------------------------------|------------------------------------------|
  | **1. Docker Installation**           | **1. Docker Installation**               |
  | **2. Initialize Docker Swarm**       | **2. Join Docker Swarm**                 |
  | ```docker swarm init``` | Paste the join command generated by Docker-Master.|
  |  Copy the join command generated by Docker-Master. | ```docker swarm join --token <token> <Master-IP-Address>:2377``` |
  | **3. Verify the Nodes**              | **3. Check Docker Images & Containers**  |
  | ```docker node ls```            | ```docker images```                 |
  |                                      | ```docker ps```                     |
  | **4. Promote Worker to Manager (Optional)** |                                          |
  | ```docker node promote <Worker-Node-ID>``` |                              |
  | ```docker service create --replicas=4 -p 8000:80 --name=login httpd``` |                              |
  | ```docker node ls```            |                  |
  | ```docker service ls```            | ```docker ps```                 |
  | **5. To do Scale Up** |                                          |
  | ```docker service scale login=8``` |                              |
  | ```docker ps```            | ```docker ps```                 |
  | **5. To do Scale Down** |                                          |
  | ```docker service scale login=2``` |                              |
  | ```docker ps```            | ```docker ps```                 |
  | ```docker service ls```            | ```docker service ls```                 |
  | ```docker service rm login``` |                              |
---

# Docker and AWS ECR Integration
## How to push Docker Image to Amazon Elastic Container Registry(AWS ECS)
This documentation covers the steps to integrate Docker with AWS Elastic Container Registry (ECR) for storing and pushing container images.

## 1 Setup and Commands
### 1.1. Configure AWS CLI
```bash
aws configure
```
- *Explanation:* This command configures the AWS CLI by prompting you to enter your AWS credentials (Access Key ID, Secret Access Key, region, and output format). This ensures that your local environment is set up for interacting with AWS services.
### 1.2. Log into AWS ECR with Docker
```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <aws account_id Number.>.dkr.ecr.ap-south-1.amazonaws.com
```
- *Explanation:* This command retrieves an authentication token for logging into AWS ECR and then pipes the token into `docker login`. It authenticates Docker to interact with the ECR registry (in this case, the `ap-south-1` region). The `--password-stdin` option securely passes the password to Docker.
### 1.3. Create ECR Repository for "hello-repository" through AWS CLI

```bash
aws ecr create-repository --repository-name hello-repository --region ap-south-1
```
- *Explanation:* This command creates a new ECR repository named `hello-repository` in the `ap-south-1` region.

### 1.4. List Local Docker Images & Tag Local Docker Image for ECR
```bash
docker images
docker tag hello-world:latest 339713104321.dkr.ecr.ap-south-1.amazonaws.com/hello-repository
```
- *Explanation:* This command tags the local `hello-world:latest` Docker image with the full ECR repository URL (`339713104321.dkr.ecr.ap-south-1.amazonaws.com/hello-repository`) to prepare it for pushing to the repository.

### 1.5. Push Docker Image to ECR
```bash
docker push 339713104321.dkr.ecr.ap-south-1.amazonaws.com/hello-repository:latest
```
- *Explanation:* This command pushes the tagged Docker image (`hello-world:latest`) to the specified repository (`hello-repository`) on AWS ECR.


## 2. Setup and Commands
### 2.1. Configure AWS CLI
```bash
aws configure
```
- *Explanation:* This command configures the AWS CLI by prompting you to enter your AWS credentials (Access Key ID, Secret Access Key, region, and output format). This ensures that your local environment is set up for interacting with AWS services.
### 2.2. Log into AWS ECR with Docker
```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <aws account_id Number.>.dkr.ecr.ap-south-1.amazonaws.com
```
### 2.3. Create ECR Repository for "hello-repository" in ECR AWS Console
- Create a Repo in Amazon Elastic Container Registry and Copy the 

### 2.4 Tag Apache Tomcat Docker Image for ECR
```bash
docker tag apache-tomcat:latest 339713104321.dkr.ecr.ap-south-1.amazonaws.com/apache-tomcat
```
- *Explanation:* This command tags the `apache-tomcat:latest` Docker image with the ECR repository URL (`339713104321.dkr.ecr.ap-south-1.amazonaws.com/apache-tomcat`).

### 2.5 Push Apache Tomcat Docker Image to ECR
```bash
docker push 339713104321.dkr.ecr.ap-south-1.amazonaws.com/apache-tomcat:latest
```
- Explanation: This command pushes the `apache-tomcat:latest` image to the `apache-tomcat` repository in AWS ECR.









