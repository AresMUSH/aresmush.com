---
title: Nginx
description: 
layout: page
tags:
- troubleshooting
---

Ares' default installation uses the Nginx web server for serving up pages from the game's web portal. (You can theoretically use any other web server in a custom install, but you're on your own; Nginx is the only supported configuration).

This is what the default nginx config will look like for a game that's using CertBot/HTTPS. You can edit it using `sudo nano /etc/nginx/sites-enabled/default`.

Note: The ports 4202 and 4203 should match the `engine_api_port` and `websocket_port` from your game server configuration (in `/home/ares/aresmush/game/config/server.yml`).

```
upstream api_upstream {
  server 127.0.0.1:4203;
  }

upstream ws_upstream {
  server 127.0.0.1:4202;
  }

server {
  listen 80 default_server;
  listen [::]:80 default_server;
  root /var/www/html;
  index index.html;
  client_max_body_size 100M;

  server_name yourgame.aresmush.com;


  listen [::]:443 ssl ipv6only=on; # managed by Certbot
  listen 443 ssl; # managed by Certbot
  ssl_certificate /etc/letsencrypt/live/yourgame.aresmush.com/fullchain.pem; # managed by Certbot
  ssl_certificate_key /etc/letsencrypt/live/yourgame.aresmush.com/privkey.pem; # managed by Certbot
  include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
  ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

  if ($scheme = "http") {
      return 301 https://$host$request_uri;
  } # managed by Certbot

    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        # try_files $uri $uri/ =404;
        try_files $uri $uri/ /index.html;
    }

  location ~ /game/(config|logs) {
   deny all;
   return 404;
  }
       
  location /websocket/ {
    proxy_pass http://ws_upstream;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header Connection "Upgrade";
    proxy_read_timeout 7d;
  }
            
    location /api/ {
    proxy_set_header HOST $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_pass http://api_upstream;
  }
    
}
```


