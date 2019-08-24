# Users and Groups

## Add a new user
```bash
useradd --create-home [name]
```

## Set password for user

```bash
passwd [name]
```

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
