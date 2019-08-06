# Cassandra

## Run

Pull and run as a Docker instance:

```
$ docker pull cassandra
$ docker run --name cassandra -p 127.0.0.1:9042:9042 -p 127.0.0.1:9160:9160  -d cassandra:latest
```

## Troubleshooting

### Fails to start

Check the output of `cassandra -f` 
