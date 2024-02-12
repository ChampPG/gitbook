# Updated Certbot Guide

## Nginx Install

```
sudo apt update
sudo apt install nginx
```

## Certbot

Resource link: https://certbot.eff.org/instructions?ws=other\&os=pip&#x20;

Install: Nginx Certbot

```
apt install python3 python3-venv libaugeas0
python3 -m venv /opt/certbot/
/opt/certbot/bin/pip install --upgrade pip
/opt/certbot/bin/pip install certbot certbot-nginx
ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```

#### Install: cloudflare plugin&#x20;

```
/opt/certbot/bin/pip install certbot certbot-dns-cloudflare
```

## Option 1: User nginx reverse proxy with certbot nginx

Make file for domain:

```
sudo nano /etc/nginx/sites-available/yourdomain.com
```

Config setup: (This config will be auto managed by cert bot)

```
server {
    listen 80;
    server_name <sub-domain>.yourdomain.com;

    location / {
        proxy_pass http://your_backend_server_address;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Now simlink your available site to enabled:

```
sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
```

Now test config and restart nginx:

```
nginx -t
systemctl restart nginx
```

### Make nginx cert

```
certbot --nginx
```

Follow instructions on screen (Adding screenshots soon)

Test cert renew:

```
sudo certbot renew --dry-run
```

## Option 2: User nginx reverse proxy with certbot cloudflare

### Cloudflare API token used by Certbot

Make .ini file for domain in:

```
/home/<user>/.secrets/certbot/
```

Contents in file:

```
dns_cloudflare_api_token = YOUR_CLOUDFLARE_API_TOKEN
```

Save and close file

Now change file permissions:

```
chmod 600 /path/to/file/<nameoffile>.ini
```

Make cert:

```
certbot certonly \
  --dns-cloudflare \
  --dns-cloudflare-credentials /home/user/.secrets/certbot/<nameoffile>.ini \
  --dns-cloudflare-propagation-seconds 60 \
  -d "*.example.com"
```

Test cert renew:

```
sudo certbot renew --dry-run
```

### Make Nginx config:

Make file for domain:

```
sudo nano /etc/nginx/sites-available/yourdomain.com
```

Config setup: (This config WON'T be auto managed by certbot)

```
server {
    listen 443 ssl http2;
    server_name <sub-domain>.yourdomain.com;

    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256';
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 1d;
    ssl_session_tickets off;
    ssl_stapling on;
    ssl_stapling_verify on;
    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header X-Content-Type-Options nosniff;
    add_header X-Frame-Options SAMEORIGIN;
    add_header X-XSS-Protection "1; mode=block";

    location / {
        proxy_pass http://your_backend_server_address;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Now simlink your available site to enabled:

```
sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
```

Now test config and restart nginx:

```
nginx -t
systemctl restart nginx
```
