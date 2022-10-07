# Load Balancing

This config has 2 servers `my.server1.com` and `my.server2.com` and combines them. Nginx proxies that group of servers under the name `http://server_group` this can be renamed. In this config it uses weight which routes 3 requests to `my.server1.com` before routing 1 to `my.server2.com`

<pre><code>http   {
  upstream server_group   {
    server my.server1.com weight=3;
<strong>    server my.server2.com;
</strong><strong>  }
</strong>  server  {  
    location / {   
        proxy_pass http://server_group;  
    }    
<strong>  }
</strong>}</code></pre>
