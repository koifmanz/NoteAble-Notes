---
tags: [Notebooks/DevOps, Notebooks/Docker]
title: Docker Basic Commands
created: '2020-09-11T07:40:03.052Z'
modified: '2021-08-18T10:41:35.108Z'
---

# Docker Basic Commands


```terminal
docker build -t <image name> .
```

build image from docker file

```terminal
docker images
```

print all images

```terminal
docker ps
docker ps -a
```

print all the containers, the flag -a include dead containers

```terminal
docker run <image name>
```
Create a contanier, more flags recomended 

```terminal
docker kill <contanier name>
```
stop contanier

```bash
docker exec -it <mycontainer> bash
docker exec -it <mycontainer> sh
```

this will let you run arbitrary commands inside an existing container

```bash
docker logs <contanier name>
```

View the logs of container, great for debugging
