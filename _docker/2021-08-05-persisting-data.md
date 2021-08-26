---
layout: episode
title: Persisting Application Data
date: 2021-08-05 01:01:01 +0530
teaching: 15
exercises: 10
objectives:
- Understand how to persist the application data
- Understand Docker volume
# keypoints:
# - Docker has commands for managing images like `docker images`, `docker rmi`, `docker build`.
# - Docker has commands for managing container like `docker run`, `docker exec`, `docker ps`, `docker inspect` etc.
# - Docker has commands for checking system or other information like `docker info`, `docker version`, `docker stats` etc.
---

In the previous episode, we saw how to run dynamic application and interact with it by updating user's information.

However, one of the issue currently is that when we restart or remove the container, then we lost the data we updated to our user.

## Overview of Docker Volume

<img src="https://docs.docker.com/storage/images/types-of-mounts.png" class="embed-img">

- We need Docker volume for data persistance.
- Folder or directory in the host file system is mounted into the virtual file system of Docker. Example:

  ~~~bash
  $ docker run -d -p 8080:80 --volume /home/username/static-app:/usr/share/nginx/html nginx
  ~~~

- There type of volume types:

  - __Host Volume:__ You decide where on the host file system the reference is made. See above example.
  - __Anonymous Volume:__ For each container, a folder is generated in the host file system that get mounted.

    ~~~bash
    $ docker run -v /var/lib/mysql/data mysql
    ~~~

    __NOTE:__ Above command is just an example and might not work. It might be stored in the host system defined by Docker like in Linux it will be mounted on `/var/lib/docker/volumes/random-hash/_data`

  - __Named Volume:__ You can reference the volume by name and it should be used in production.

    ~~~bash
    $ docker run -v app-db:/var/lib/mysql/data mysql
    ~~~

    __NOTE:__ Above command is just an example and might not work. It might be stored in the host system defined by Docker like in Linux it will be mounted on `/var/lib/docker/volumes/random-hash/_data`
