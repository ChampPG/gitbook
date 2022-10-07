# Nginx

### Documentation

{% embed url="https://nginx.org/en/docs/" %}
Nginx Config Documentation
{% endembed %}

{% embed url="https://docs.nginx.com/" %}
Product Documentation
{% endembed %}

### Installation

1. `apt-get install nginx`
2. `sudo unlink /etc/nginx/sites/enabled/default` - This makes it so the default config won't be used anymore
3. `cd /etc/nginx/sites-available/`

&#x20;      \* sites-available is where you put configs that can be used for later

&#x20; 4\. `sudo nano {name}.conf` - This will create the new config file

&#x20; 5\. Make config. Config references can be down under the Subsections tab

&#x20; 6\. `ln -s /etc/nginx/sites-available/{name}.conf /etc/nginx/sites-enabled/{name}.conf` - This will enable the Nginx config

### Testing and Restart Nginx

* `nginx -t -c /etc/nginx/{name}.conf` - This will test the config file
* `systemctl restart nginx` - Will restart the Nginx service and enable the config in `sites-enabled`
