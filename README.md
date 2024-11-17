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
  **Pull one httpd image and run a container & stop the container and restart the container and remove the docker image.**
  ```
docker images    ##Lists available images on the system; used to check image availability.
docker ps    ##Shows running containers; used to monitor active containers.  
docker pull httpd    ##Downloads the ```httpd``` image from Docker Hub; used to prepare an image.
docker images
docker run -it -d httpd
docker ps
docker rm container_id
docker stop container_id
docker ps -a
docker start container_id
docker stop container_id
docker rm container_id
docker ps -a
docker images
docker rmi httpd
docker images
```

  ## Task-2
  ## Task-3
  ## Task-4
  ## Task-5

# Docker-Compose Setup on Linux
  ```sh
  sudo yum install git -y
  sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose 
  sudo chmod +x /usr/local/bin/docker-compose
  docker-compose --version
  ```
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
