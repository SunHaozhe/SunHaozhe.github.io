---
layout: post
category: Misc     
title: Docker memo 
tagline: by SunHaozhe
tags: 
  - API  
  - Utilities 
  - Common knowledge
mathjax: true
comments: true
published: true
---

# General information 

Show the Docker version information 

```zsh
docker version
```

Display system-wide information

```zsh
docker info 
```

Display a live stream of container(s) resource usage statistics

```zsh
docker stats
```

# Docker image

Build an image from the Dockerfile in the current directory and tag the image

```zsh
docker build -t myimage:1.0 
```

Pull an image from a registry

```zsh
docker pull myimage:1.0 
```

Retag a local image with a new image name and tag

```zsh
docker tag myimage:1.0 myrepo/myimage:2.0 
```

Push an image to a registry 

```zsh
docker push myrepo/myimage:2.0 
```

List all images that are locally stored with the Docker Engine

```zsh
docker image ls
```

Delete an image from the local image store

```zsh
docker image rm [imageName]
docker image rm alpine:3.4 # an example 
```

# Docker container 

List containers (only shows running)

```zsh
docker ps
```

List all containers (including non-running)

```zsh
docker ps -a
```

List the running containers (add `--all` to include stopped containers) 

```zsh
docker container ls 
```

Run a container from the Alpine version 3.9 image, name the running container `web` and expose port 5000 externally, mapped to port 80 inside the container

```zsh
docker container run --name web -p 5000:80 alpine:3.9
```

# Network 

List the networks 

```zsh
docker network ls 
```


# Example 


Docker image sunhaozhe/pytorch-cu100-jupyter-gym:
	* linux Ubuntu 18.04
	* python 3.6.8
	* pytorch for GPU (cuda 10.0)
	* jupyter, configure jupyter notebook for remote connection
	* pip install gym 
	* apt-get update
	* apt-get install nano
	* apt install tmux
	* pip install visdom 
	* pip install --upgrade pip 
	* pip install tensorboard 
	* pip install tensorboardx (No !!!!!!!)
	* git clone https://github.com/lanpa/tensorboardX && cd tensorboardX && python setup.py install 

Docker image sunhaozhe/pytorch-cu100-gym-tmux-tensorboardx:
	* pip install --upgrade pip
	* pip install gym
	* apt-get update
	* apt-get install nano
	* apt install tmux
	* pip install tensorflow (not only tensorboard because reduced feature set)
	* git clone https://github.com/lanpa/tensorboardX && cd tensorboardX && python setup.py install


all-in-one with jupyter, CPU-only / Python 3.

```zsh
docker pull ufoym/deepo:all-py36-jupyter-cpu
```

all-in-one with jupyter, CUDA 10.0 / Python 3.6

```zsh
docker pull ufoym/deepo:all-jupyter-py36-cu100
```

```zsh
docker run -dit --name my_env --mount 
type=bind,source=C:\xxx\yyy\zzz\workspace,target=/workspace 
sunhaozhe/pytorch-cu100-gym-tmux-tensorboardx
```

* `-p 18888:8888` for jupyter notebook 
* `-p 8097:8097` for visdom server
* `-p 6006:6006` for tensorboardx 


```zsh
docker exec -it my_env bash
```





# References 

* http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html












































































