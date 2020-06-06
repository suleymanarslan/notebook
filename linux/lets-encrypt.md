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

## Wildcard 

```
sudo certbot --server https://acme-v02.api.letsencrypt.org/directory -d *.example.com --manual --preferred-challenges dns-01 certonly
```

```
server {
  listen 80;
  listen [::]:80;
  server_name *.example.com;
  return 301 https://$host$request_uri;
}

server {
  listen 443 ssl;
  server_name *.example.com;  ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
  include /etc/letsencrypt/options-ssl-nginx.conf;
  ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;  root /var/www/example.com;
  index index.html;
  location / {
    try_files $uri $uri/ =404;
  }
}
```
