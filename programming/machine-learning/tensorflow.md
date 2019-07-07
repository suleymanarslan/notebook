# TensorFlow

## Start Model Server

```bash
$ docker run -t --rm -p 8501:8501 \
    -v "/home/azer/models/fuji/model:/models/fuji" \
    -e MODEL_NAME=fuji -e GRPC_VERBOSITY=DEBUG -e GRPC_GO_LOG_VERBOSITY_LEVEL=2 -e GRPC_TRACE=all  \
    tensorflow/serving
```

Get metadata of a model:

```bash
$ curl localhost:8501/v1/models/fuji/versions/0001/metadata
```

## Start a Jupyter Notebook Server

```
$ docker run -it -p 8888:8888 tensorflow/tensorflow:0.10.0rc0
```
