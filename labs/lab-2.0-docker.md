# Lab 2.0: Docker

### Summary

This lab was extremely useful for me because I have tried to install Docker before on a fedora server and didn't understand anything at all. So being able to go over it and actually have well formatted steps I can now say I can understand somewhat how to use Docker and Docker-Compose.

### Ubuntu Network Configuration

1. Get network adapter name by using `ip addr`
2. Edit the file `/etc/netplan/00-installer-config.yaml`
3. Edit the file to look like below without ()

```
network:
  version: 2
  renderer: networkd
  ethernets:
    (**adapter name**):
     addresses: [(**ip**)/(**subnet**)]
     gateway4: gateway
     nameservers:
       addresses: [(**dns server ip**)]
```

1. now run `sudo netplan apply` or `sudo netplan try` (if unsure) hit `Enter` when prompted

### Making A New Sudo User

* Make a new user with a user directory `useradd -m USERNAME`
* Make this account an admin `sudo usermod -aG sudo USERNAME`

### Docker Commands

* `docker version` | check docker version
* `docker-comopose --version` | check docker-compose version
* `sudo usermod -aG docker USERNAME` | To add user to docker group
* `docker run hello-world` | test if docker is working
* `docker run --rm PACKAGE:latest` | will run the latest version of a package
  * The `--rm` means the container will automatically be removed when the container is exited
* `docker run NAME` | run the specific container
  * `docker run -d -P` | will run container | -d (--detach) means run container in the background and print container ID | -P (–publish-all) means Publish all exposed ports to random ports
* `docker stop NAME` | stop the specific container
* `docker images` | lists all local images on the host
* `docker ps` | lists all running containers
  * `docker ps -a` | will list all containers even running
* `sudo chmod +x /usr/local/bin/docker-compose` | allows you to run docker-compose
* `docker-compose up` | run docker docker-compose.yml file in current directory
* `docker-compose down` | stop docker docker-compose.yml file in current directory
