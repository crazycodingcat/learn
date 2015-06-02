##### Important note for our local setup:
1. Must use alpha network. Otherwise the docker image will have problem accessing internet.
2. The flask application must use host='0.0.0.0'. This allows us to access the app's port from outside of the container.

### Step 0: Generate requirements.txt for your app
The packages listed in requirements.txt will be installed to the base image during the build process.

### Step 1: Add a Dockerfile in your application's directory
DockerFile is a script that houses instructions needed to create an image. The image can then be created based on the instructions in the DockerFile using the Docker build command. It simplifies deployment of an image by easing the entire image and container creation process. 

Sample Dockerfile:
```
# Specify the base image
FROM ubuntu:14.04

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
CMD ["python", "/src/run.py"]
```

### Step 2: Build the Docker image
```
docker build -t <name of your image> .
```
-t is for tagging the image  
E.g. `docker build -t hello-flask`

### Step 3: Run a container from the image
```
docker run -d \
-e <environment variable name>:<value> \
-p <the port you want to map to on your host machine>:<the port in the container> \
<name of your image>
```
E.g. `docker run -d -p 5010:5000 hello-flask`


#### Dockerfile commands cheatsheet:
* MAINTAINER: Set an author field for the image using this instruction. The simple and obvious syntax is:
```
MAINTAINER <author name>
```
* RUN: Execute a command in a shell or exec form. The RUN instruction adds a new layer on top of the newly created image. The committed results are then used for the next instruction in the DockerFile.
```
RUN <command>
```
* ADD: Copy files from one location to another using the ADD instruction. It takes two arguments <source> and <destination>. The destination is a path in the container. The source can be either a URL or a file in the context of the launch config.
```
ADD <src> <destination>
```
* CMD: Defaults for an executing container are provided using the CMD command. DockerFile allows usage of the CMD instruction only once. Multiple usage of CMD nullifies all previous CMD instructions. CMD comes in three flavours:
```
CMD ["executable","param1","param2"] #exec form, this is the preferred form

CMD ["param1","param2"] #as default parameters to ENTRYPOINT

CMD command param1 param2 #shell form
```
* EXPOSE: Specify the port on which the container will be listening at runtime by running the EXPOSE instruction.
```
EXPOSE <port>
```
* ENTRYPOINT: Configure a container to run as an executable, which means a specific application can be set as default and run every time a container is created using the image. This also means that the image will be used only to run and target the specific application each time it is called.

Similar to CMD, #Docker allows only one ENTRYPOINT and multiple ENTRYPOINT instructions nullifies all of them, executing the last ENTRYPOINT instruction.

Syntax: Comes in two flavours
```
ENTRYPOINT [‘executable’, ‘param1’,’param2’]
ENTRYPOINT command param1 param2
```
* WORKDIR: Working directory for the RUN, CMD and ENTRYPOINT instructions can be set using the WORKDIR.
```
WORKDIR /path/to/workdir
```
* ENV: Set environment variables using the ENV instruction. They come as key value pairs and increases the flexibility of running programs.
```
ENV <key> <value>
```
* USER: Set a UID to be be used when the image is running.
```
USER <uid>
```
* VOLUME: Enable access from a container to a directory on the host machine.
```
VOLUME [‘/data’]
```
#### Dockerfile best practices
A. Keep common instructions like MAINTAINER and update commands right on top of the DockerFile;

B. Use human readable tags while building the images to better manage images;

C. Avoid mapping the public port in a DockerFile;

D. As a best practice, use array syntax for CMD and ENTRYPOINT.


###### Sources:   
- http://blogs.aws.amazon.com/application-management/post/Tx1ZLAHMVBEDCOC/Dockerizing-a-Python-Web-App
- http://docs.docker.com/reference/builder  
- http://blog.flux7.com/blogs/docker/docker-tutorial-series-part-3-automation-is-the-word-using-dockerfile
