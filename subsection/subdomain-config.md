# Subdomain Config

This will create a config that has 3 different service on port 80 with different subdomains.

```
server {
    listen 80;
    server_name admin.domain.com;
    location / {
        proxy_set_header Host $host;
        proxy_pass http://127.0.0.1:3434;
        proxy_redirect off;
    }
}
server {
    listen 80;
    server_name user.domain.com;
    location / {
        proxy_set_header Host $host;
        proxy_pass http://127.0.0.1:3435;
        proxy_redirect off;
    }
}
server {
    listen 80;
    server_name vendor.domain.com;
    location / {
        proxy_set_header Host $host;
        proxy_pass http://127.0.0.1:3436;
        proxy_redirect off;
    }
}   
```
