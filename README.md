# LAMP Installation With Joomla Front End
This repository contains a dockerfile that will create an image with a LA[M]P backend and Joomla front end. This
build uses the following infrastructure:
 L: Ubuntu 16.04 Stable
 A: Apache 2 - Latest
 M: No MySql installation with this, I suggest following the instructions below for the MySql portion
 P: PHP 7 - Latest
 Joomla: 3.5.1

# Installation
1. Copy the repo in a local directory.
2. Run "docker build <path/to/DockerFolder/Docker/>"
3. Once built, run "docker run -p 80:443 -d --name <container name> <container id>"

# Gather your Docker-machine IP
Depending on what environment you are running, you will run something like the following.
Note: Default is the typical env running if you have not set up something specific.

Run "docker-machine ip default"

You should then be able to visit your Joomla Instance by going to the url:
http://<docker-machine env ip>/:80

# I see my default Joomla Page, now what?
Go ahead and go through the set up to install Joomla within your container. You will need to have you MySql container
up and running by that point, with knowledge of its IP and the database that you will use.

# MySql Instructions

1. Build the MySql Image from DockerHub, this also runs the container.
      "docker run --name <image_name> -e MYSQL_ROOT_PASSWORD=<root password> -d  -p 3306:3306 mysql:latest"

You are essentially building the image from an established Dockerfile that lives within Dockerhub. This established
image has the appropriate code to not only create the Docker image, but also initialize a container based on
the information you pass to it. I could be wrong here though.

2. Once finished, you will be able to connect with your MySql box via SQLPro or any method you like through the
  docker-machine ip with port 3306.
