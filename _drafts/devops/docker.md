---
layout: post
title: "Docker"
category: jekyll update
---

![need-update docker]({{site.base_url}}/_images/docker.png)

### Concepts
#### Docker Daemon (dockerd)
Docker daemon listens to REST API on docker client and manages docker objects (image, container, volume, network, ..). A daemon can talk to other docker daemon to manage services.

#### Docker Client (docker)
Docker client sends command (run, image, cp ..) to one or more docker daemon to carry out.

#### Docker Registry
Stores docker image. When docker run or docker pull command is run it pulls necessary image from docker registry.

#### Docker Objects
##### Image
Image is read-only template with instructions for creating docker container. Dockerfile is used for creating docker images manually. Dockerfile starts with a base docker image and additional instruction are added on it which is called layer. When creating container from image only the layer that has been changed rebuilt making docker image fast and lightweight.

##### Container
Runnable instance of a docker image that is sufficiently separated from it’s host and other container.

> Docker uses a technology called namespaces to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container.
>
> These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace

container in-depth:
- [Containers From Scratch • Liz Rice • GOTO 2018][docker container-scratch] 
- [Demystifying Containers - Part I: Kernel Space][docker container-demystify] 

##### Volume
Generally each container gets it’s own scratch space for filesystem and is not visible to other container or host machine. We can use volume to map specific filesystem path back to host machine. 

- named volume: 
  - create the volume → 
{% highlight bash %}
docker volume create named-db
{% endhighlight %}

  - create container using the named volume → 
{% highlight bash %}
docker run -it -v named-db:/opt/blah/bla ubuntu:latest /bin/bash
{% endhighlight %}

  - it will mount the `opt/blah/bla`` path of container to named-db volume. To know it’s exact location on host we can run the following command to get the Mountpoint -
{% highlight bash %}
docker volume inspect name-db
{% endhighlight %}

named volume populate the new volume with container contents(?) and also supports other volume drivers such as SFTP, Ceph, NetApp, S3, etc.

- bind mount:
bind mount is another type of volume where we can specify Mountpoint in host machine. 
{% highlight bash %}
mkdir /opt/vol1
docker run -it -v /opt/vol1:/opt/blah/bla ubuntu:latest /bin/bash 
{% endhighlight %}

the difference between named volume and bind mount also that bind mount does not populate new volume with container contents(?) and does not support other volume driver.

##### Network
For multi-container application it is important that all container be at same network for them to be able to talk to each other.

- create the network → 
{% highlight bash %}
docker network create test-network
{% endhighlight %}

- create a container in the created network → 
{% highlight bash %}
docker run -it --network test-network --network-alias test ubuntu:latest /bin/bash
{% endhighlight %}

#### Docker-compose
Docker-compose help define and distribute multi-container service. It uses YAML config file to define container setup. 

run docker-compose configuration → 
{% highlight bash %}
docker-compose <yml file> up
{% endhighlight %}

tear down docker-compose configuration → 
{% highlight bash %}
docker-compose <yml file> down
{% endhighlight %}

##### Syntax

#### Dockerfile
##### Image Building Best Practices

- Security Scanning
{% highlight bash %}
docker scan <container name>
{% endhighlight %}

- Image Layering
{% highlight bash %}
docker image history --no-trunc <image name>
{% endhighlight %}

- Layer Caching
> Once a layer changes all the downstream layer needs to recreated as well

- Multi-stage Build

>  - Separate build time dependencies from runtime dependencies
>  - Reduce the size of the image by shipping only what is needed

#### Orchestration
In production it is not possible to just simply run docker run or docker-compose up. There are lot of things to consider such as what if the container dies. There are lot of tools that is built to manage that - 

- kubernetes
- Swarm
- Nomad
- ECS

### Commands
{% highlight bash %}
docker run
docker exec
docker image
docker ps
docker volume [create|inspect]
docker network [create]
docker 
{% endhighlight %}

### Sources
https://docs.docker.com/get-started/overview/

[docker container-scratch]: https://www.youtube.com/watch?v=8fi7uSYlOdc
[docker container-demystify]: https://medium.com/@saschagrunert/demystifying-containers-part-i-kernel-space-2c53d6979504