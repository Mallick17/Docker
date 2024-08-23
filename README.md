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

# Docker-Compose Setup on Linux
  ```sh
  sudo yum install git -y
  sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose 
  sudo chmod +x /usr/local/bin/docker-compose
  docker-compose --version
  ```
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
