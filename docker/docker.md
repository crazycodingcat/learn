### VM vs. Container
<img src="https://s3.amazonaws.com/serversforhackers/difference.png" width="500">

### Docker vocabulary
<img src="https://s3.amazonaws.com/codementor_content/2015-Feb-week1/docker_vs_git.png" width="400">

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
* --name="your container name"

#### See all containers       

```
sudo docker ps -a
```
#### Remove containers/images 
- To remove a container: `docker rm <Container ID>`   
- To remove all containers: `docker rm $(docker ps -a -q)`   
- To remove images: `docker rmi <Container ID>`
- To remove all images: `docker rmi $(docker ps -a -q)`

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
```
FROM ubuntu:12.10

# Install Python Setuptools
RUN apt-get install -y python-setuptools

# Install pip
RUN easy_install pip

# Add and install Python modules
ADD requirements.txt /src/requirements.txt
RUN cd /src; pip install -r requirements.txt

# Bundle app source
ADD . /src

# Expose
EXPOSE  5000

# Run
CMD ["python", "/src/application.py"]
```

### Notes:
- A Docker container only stays alive as long as there is an active process being run in it.
- The sort of rule of thumb in the Docker world is to have one Docker container running on your server for each process in your stack. This isn’t a hard rule, but it’s a good one for people who are just starting out.
<img src="https://s3.amazonaws.com/codementor_content/2015-Feb-week1/runningc.png" width="500">

### Troubleshooting
##### Problem: Docker container cannot connect to internet: Could not resolve 'archive.ubuntu.com'
Solution: Sometimes docker is unable to use the host OS's DNS resolver, resulting in a DNS resolve error within your Docker container. We can fix this by explicitly telling Docker to use Google's DNS public server (8.8.8.8).
###### Step 1. Add to /etc/default/docker:   
`DOCKER_OPTS="--dns 8.8.8.8 --dns 192.168.100.102"`.  
###### Step 2. Find and explicitly add the network's DNS server as a backup as well:     
*(Optional, used if your network blocks all public DNS)*  
How: 
1. From the host OS, check the address of the DNS server you're using locally with nm-tool, e.g.:
```
$ nm-tool
...
  IPv4 Settings:
    Address:         192.168.100.154
    Prefix:          21 (255.255.248.0)
    Gateway:         192.168.100.101

    DNS:             192.168.0.1  # This is my DNS server address
...
```
2. Add your DNS server as a 2nd DNS server for Docker
```
# /etc/default/docker
# ...
# Use DOCKER_OPTS to modify the daemon startup options.
DOCKER_OPTS="--dns 8.8.8.8 --dns 192.168.0.1"
# Google's DNS first ^, and ours ^ second
```
###### Step 3. Restart Docker  
`sudo service docker restart`

Sources: 
- https://serversforhackers.com/getting-started-with-docker
- https://www.codementor.io/docker/tutorial/what-is-docker-tutorial-andrew-baker-oreilly
- https://robinwinslow.co.uk/2014/08/27/fix-docker-networking/


