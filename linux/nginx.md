# Nginx

## Set password protection

Generate `htpasswd`:

```bash
$ echo -e "your-username:`perl -le 'print crypt("your-password","salt")'`" > /etc/nginx/htpasswd
```

Point it in the configuration:

```bash
auth_basic           “Administrator’s Area”;
auth_basic_user_file /etc/nginx/htpasswd; 
```
