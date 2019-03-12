# Users and Groups

## See list of groups user belongs to

```
groups $USER
```

## Create a new group

```
groupadd fun
```

## Add user to a group

```
usermod -a -G fun $USER
```
