# Docker

## List All Processes

```bash
$ docker ps -a
```

or

```bash
$ docker container ls -a
```

Now you can restart a stopped container:

```bash
$ docker restart $container_id
```

## Pull and run an image

```bash
$ docker run -it -p 8888:8888 tensorflow/tensorflow:0.10.0rc0
```

## `run`

#### Run a command in a new named container

```bash
$ docker run --name [name] [options] [image]
```

#### Detached Container

Run the container as a background process (a.k.a detached mode)

```bash
$ docker run -d [image]
```

#### Publish Port

```bash
$ docker run -p [host-port]:[container-port] [image]
```

#### Mount host volumes

```bash
$ docker run -v [host-path]:[container-path] [image]
```

## List all images

```bash
$ docker image ls
```

## Clean all containers

```bash
$ docker rm $(docker ps -aq)
```

## Run command

```bash
$ docker exec -it <container name> <command>
```

## Open up terminal

```bash

$ docker exec -it <container name> /bin/bash
```

## Stop all containers

```bash
$ docker stop $(docker ps -aq)
```

## Remove images matching pattern

```bash
$ docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi
```

## Remove containers matching pattern

```bash
$ docker ps -a | grep "pattern" | awk '{print $1}' | xargs docker rm
```
