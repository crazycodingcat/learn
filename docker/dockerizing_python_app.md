##### Important note for our local setup:
1. Must use alpha network. Otherwise the docker image will have problem accessing internet.
2. The flask application must use host='0.0.0.0'. This allows us to access the app's port from outside of the container.

### Step 0: Generate requirements.txt for your app
The packages listed in requirements.txt will be installed to the base image during the build process.

### Step 1: Add a Dockerfile in your application's directory
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

###### Sources:   
http://blogs.aws.amazon.com/application-management/post/Tx1ZLAHMVBEDCOC/Dockerizing-a-Python-Web-App
