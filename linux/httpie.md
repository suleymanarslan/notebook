# HTTPIE

A simple request:

```bash
$ http httpie.org
```

Custom headers and JSON data:

```bash
$ http PUT example.org X-API-Token:123 name=John
```

Submit form:

```bash
$ http -f POST example.org hello=World
```
