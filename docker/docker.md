### VM vs. Container
![image vm vs container]
(https://s3.amazonaws.com/serversforhackers/difference.png)

### Commands:
```
docker run -t -i ubuntu /bin/bash
```
* docker run - Run a container
* -t - Allocate a (pseudo) tty
* -i - Keep stdin open (so we can interact with it)
* ubuntu - use the Ubuntu base image
* /bin/bash - Run the bash shell


### Notes:
- A Docker container only stays alive as long as there is an active process being run in it.
