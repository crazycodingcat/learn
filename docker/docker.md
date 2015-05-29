### VM vs. Container
![image vm vs container]
(https://s3.amazonaws.com/serversforhackers/difference.png)

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

### Notes:
- A Docker container only stays alive as long as there is an active process being run in it.
