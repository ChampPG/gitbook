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

Config setup:

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

Make file for domain:

```
sudo nano /etc/nginx/sites-available/yourdomain.com
```

Config setup:

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
