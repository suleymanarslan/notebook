# Cassandra

## Run

Pull and run as a Docker instance:

```bash
$ docker pull cassandra
$ docker run --name cassandra -p 127.0.0.1:9042:9042 -p 127.0.0.1:9160:9160  -d cassandra:latest
```

Run commands inside the container:

```bash
$ docker exec -it cassandra bash
```

Logs

```bash
$ docker logs some-cassandra
```

## Troubleshooting

### Fails to start

Check the output of `cassandra -f` 
