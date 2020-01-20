# Chmod

Print numerical permission value of a file / folder:

```bash
$ stat --format '%a' <file>
```

Change permissions of a file: 

```bash
$ chmod 0700
```

Add specific permissions to existing value;

```bash
$ chmod +wx file 
```
