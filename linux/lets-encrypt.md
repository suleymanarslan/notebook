# Let's Encrypt

Install `certbot`:

```
$ sudo apt-get install certbot python-certbot-nginx
```

Generate certificate and update the nginx config;

```
$ sudo certbot --nginx
```

Create a cronjob to renew the certificate daily:

```
43 6 * * * certbot renew --post-hook "systemctl reload nginx"
```
