---
layout: post
title: Common Cammander of Docker
subtitle: Docker学习笔记系列
date: 2019-05-27
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - Docker
---

#### list all running containers
```
docker ps
```

#### list all existed containers
```
docker ps -a
```

#### stop container
```
docker stop <container id>
```

#### delete container
```
docker rm <container id>
```

#### list all images
```
docker images
```

#### building your image
```
docker build -t <image name> .
```

#### run your image
The `-p` flag redirects a public port to a private port inside the container.<br/>
`-d` is meant to run the container in detached mode
```
docker run -p <public port>:<private port> -d <image name>
```

#### delete a images
```
docker rmi <images id>
```

#### log app output
```
docker logs <container id>
```

#### If you need to go inside the container you can use the exec command:
```
docker exec -it <container id> /bin/bash
```
