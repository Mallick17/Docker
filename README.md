# Docker

## Docker & Docker-Compose Setup on Amazon Linux
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

---

## Docker & Docker-Compose Setup on Ubuntu 22.04 LTS
### 1. Set up Docker's `apt` repository
- Follow these steps to configure the repository:
```sh
# Update package index and install prerequisites:
sudo apt-get update
sudo apt-get install -y ca-certificates curl

# Create a directory for Docker's GPG key:
sudo install -m 0755 -d /etc/apt/keyrings

# Download Docker's official GPG key:
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add Docker's repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update the package index again:
sudo apt-get update
```

### 2. Install Docker packages
- Install the latest version of Docker Engine and its components:
```sh
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 3. Check Docker Status
- Verify that Docker and containerd services are running:
```sh
sudo systemctl status docker
sudo systemctl status containerd
```
- If either service is inactive, start them using:
```sh
sudo systemctl start containerd
sudo systemctl start docker
```

### 4. Install Docker Compose
- Install Docker Compose in EC2
```sh
sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
- Verify Installations
```sh
docker --version
docker-compose --version
```










