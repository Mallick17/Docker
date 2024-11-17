# Docker
Commands and Installation and Study Notes
### Installation of Docker Commands
# Docker Setup on Linux
  ```sh
  sudo yum update -y
  sudo yum search docker
  sudo yum info docker
  sudo yum install -y docker
  sudo systemctl enable docker.service
  sudo systemctl start docker.service
  sudo systemctl status docker.service
  docker --version
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

# Optional: View the history of commands executed
history                                     ## Displays the history of commands executed in the terminal.


# Docker-Compose Setup on Linux
  ```sh
  sudo yum install git -y
  sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose 
  sudo chmod +x /usr/local/bin/docker-compose
  docker-compose --version
  ```
</details>

  ## Task-1
  
# Docker-File Setup on Linux
  ```sh
 
  yum install wget -y
  wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz
  yum install tar -y 
  yum install gzip -y
  tar -zxvf apache-tomcat-9.0.91.tar.gz
  yum install java-11* -y
  sh /apache-tomcat-9.0.91/bin/startup.sh
  ``` 
# Hands On Docker-File Setup on Linux
  ```sh
  FROM amazonlinux
  MAINTAINER "gyanaranjanmallick444@gmail.com"
  RUN yum install wget -y
  RUN wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz
  RUN yum install tar -y 
  RUN yum install gzip -y
  RUN tar -zxvf apache-tomcat-9.0.91.tar.gz
  RUN yum install java-11* -y
  RUN sh /apache-tomcat-9.0.91/bin/startup.sh
  ```
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
