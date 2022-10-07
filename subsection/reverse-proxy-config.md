# Reverse Proxy Config

What is shown below is a reverse proxy for the GUI of a Proxmox install. the `upstream proxmox` is used under the server section for the `proxy_pass` Other thing to note is the `server_name` is the name that you want for the proxy to be going to.

<pre><code><strong>upstream proxmox {
</strong>    server 10.10.10.10:8006;
}

server {
    listen 80 default_server;
    rewrite ^(.*) https://$host$1 permanent;
}

server {
    listen 443;
    server_name https://proxmox.domain.com;
    ssl on;
    ssl_certificate /etc/nginx/ssl/cert.pem;
    ssl_certificate_key /etc/nginx/ssl/key.pem;
    proxy_redirect off;
    location / {
        proxy_pass https://proxmox;
    }
}</code></pre>
