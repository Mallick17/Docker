# Docker
Commands and Installation and Study Notes
# Docker
Docker & Docker-Composer Installation and forecoming commands.
### Installation of Docker Commands

This is an example of how to list things you need to use the software and how to install them.
* Docker Installation Commands for Linux Server in .sh file.
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

* Docker-Compose Installation Commands for Linux Server in .sh file.
  ```sh
  sudo yum install git -y
  sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose 
  sudo chmod +x /usr/local/bin/docker-compose
  docker-compose --version
  ```
* Hands on Docker-File in Docker for Linux in .sh file
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
* Docker-File in Docker for Linux in .sh file.
  ```sh
 
  yum install wget -y
  wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz
  yum install tar -y 
  yum install gzip -y
  tar -zxvf apache-tomcat-9.0.91.tar.gz
  yum install java-11* -y
  sh /apache-tomcat-9.0.91/bin/startup.sh
  ```
* Docker-Swarm in Docker for Linux using commands on Docker-Master & Docker-Worker.
  
  | Docker-Master  | Docker-Worker |
  | ------------- | ------------- |
  | Content Cell  | Content Cell  |
  | Content Cell  | Content Cell  |
