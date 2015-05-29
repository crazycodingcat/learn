Sources: 
- https://serversforhackers.com/getting-started-with-docker
- https://www.codementor.io/docker/tutorial/what-is-docker-tutorial-andrew-baker-oreilly

### VM vs. Container
![image vm vs container]
(https://s3.amazonaws.com/serversforhackers/difference.png)

### Docker vocabulary
![vocab]
(https://s3.amazonaws.com/codementor_content/2015-Feb-week1/docker_vs_git.png)

### Commands:
#### Run a container    
```
docker run -t -i ubuntu /bin/bash
```
* docker run - Run a container
* -t - Allocate a (pseudo) tty
* -i - Keep stdin open (so we can interact with it)
* ubuntu - use the Ubuntu base image
* /bin/bash - Run the bash shell

#### See all containers       

```
sudo docker ps -a
```
#### Remove containers/images 
To remove a container: docker rm <Container ID>
To remove all containers: docker rm $(docker ps -a -q)
To remove images: docker rmi <Container ID>
To remove all images: docker rmi $(docker ps -a -q)

#### Make changes to the base image     

```
# Get into Bash
docker run -t -i ubuntu /bin/bash

# Install some stuff
apt-get update
apt-get install -y git ack-grep vim curl wget tmux build-essential python-software-properties
```
#### Commit the changes to a new image:         
```
docker commit <Container ID> <Name>:<Tag>
```

### Dockerfile
The Dockerfile provides a set of instructions for Docker to run on a container. This lets us automate installing items - we could have used a Dockerfile to install git, curl, wget, etc.

### Notes:
- A Docker container only stays alive as long as there is an active process being run in it.
- The sort of rule of thumb in the Docker world is to have one Docker container running on your server for each process in your stack. This isn’t a hard rule, but it’s a good one for people who are just starting out.
![diagram]
(https://s3.amazonaws.com/codementor_content/2015-Feb-week1/runningc.png)

