## Dockerfile to Create an Image with scikit learn and jupyter notebook Dependencies
This repo has a Dockerfile for python 3, scikit-learn, and Jupyter configured to access the app folder contents on host.   


### Usage:
Docker is essentially like a VM (Virtual Machine), but much lighter. 

Running this command, in the folder containing the Docker file   
('.' stands for current folder):
```bash
docker build -t mlnb .
```
- creates an image (similar to a VM disk image) based on this Dockerfile,
- with a name/tag "mlnb" (chose it for "machine learning notebook"),

To see available images on your system:
```bash
docker image ls
```

This Docker run command:
```bash
docker run -p 9999:8888 \
--mount 'type=bind,src="$(date)"/app,target=/app' mlnb
```
- creates a new instance for "mlnb" image and runs it
- maps internal port 8888 to the host's 9999 and 
- bind mounts the app folder in this folder to app folder in the docker container 

To list running instances
```bash
docker ps
```

To make a terminal connection to a running instance:
```bash
docker exec -it <containerName> /bin/bash
```

### More
You can study my Docker Workshop:
https://github.com/ATLD/docker_workshop

### Serving jupyter notebook as a Slideshow
In folder containing the notebook:
```bash
 git submodule add https://github.com/hakimel/reveal.js.git reveal.js
 jupyter nbconvert "<notebook name>.ipynb" --to slides --post serve
```

Also add 8000 to mapped internal ports when starting this image
```bash
docker run -p 9999:8888 -p 9000:8000 \
--mount 'type=bind,src="$(date)"/app,target=/app' mlnb
```
