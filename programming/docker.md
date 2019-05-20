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

## Clean all

```
docker rm $(docker ps -aq)
```
