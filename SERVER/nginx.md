`sudo apt install nginx`
`cd /etc/nginx/sites-enabled`     -> default holds default settings of server ..... root /var/www/html
  * `unlink default`  -> to unlink default before creating new one
`cd /etc/nginx/conf.d`  -> set new config file
  * `sudo nano new_sites.conf`  -> create new file

`nginx -t` to test
`systemctl reload nginx`
`systemctl status nginx`

if I want to set root from nginx, I have to change folder user to www-data

### stromy
```
server{
  server_name stromy.mojacz.com;
  index index.html;
  root /home/ubuntu/SERVER/Vyznamne-stromy/clientApp/dist/clientApp/;
  listen 80;
  location / {
    try_files $uri$args $uri$args/ /index.html;
  }
}
server{
  server_name stromy.admin.mojacz.com;
  index index.html;
  root /home/ubuntu/SERVER/Vyznamne-stromy/clientAdmin/dist/clientAdmin;
  listen 80;
  location / {
    try_files $uri$args $uri$args/ /index.html;
  }
}
```

### MealPlanner
```
server{
  server_name mealplan.mojacz.com;
  index index.html;
  root /home/ubuntu/SERVER/MealPlanner/MealPlannerApp/dist/MealPlannerApp/;
  listen 80;
  location / {
    try_files $uri$args $uri$args/ /index.html;
  }
}
server{
  server_name mealplan.admin.mojacz.com;
  index index.html;
  root /home/ubuntu/SERVER/MealPlanner/MealPlannerAdmin/dist/MealPlannerAdmin;
  listen 80;
  location / {
    try_files $uri$args $uri$args/ /index.html;
  }
}
```

### vocabulary.conf
```
server {
  listen 80;
  server_name vocabulary.mojacz.com;
  return 301 https://vocabulary.mojacz.com;
}

server {
  listen   443 ssl;
  server_name vocabulary.mojacz.com;

  ssl_certificate    /etc/nginx/ssl/vocabulary_mojacz_com/vocabulary_mojacz_c$
  ssl_certificate_key    /etc/nginx/ssl/vocabulary_mojacz_com/vocabulary_moja$

  location / {
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass http://localhost:8081;
  }
}
```
### other

```
server{
  server_name mojacz.com;
  listen 80 default_server;
  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass http://localhost:8080;
  }
}

server{
  server_name songsbook.mojacz.com
  listen 80;

  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass http://localhost:8082;
  }
}
server{
  server_name climbing.mojacz.com
  listen 80;
  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass http://localhost:8083;
  }
}
server{
  server_name code.mojacz.com
  listen 80;
  location / {
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass http://localhost:8084;
  }
}
```

### owncloud
```
upstream php-handler {
  server 127.0.0.1:9000;
}
server {
  server_name cloud.mojacz.com;
  listen 80;
  root /var/www/owncloud/;
  #add_header Strict-Transport-Security "max-age=15552000; includeSubDomains; preload" always;
  add_header X-Content-Type-Options nosniff always;
  add_header X-Frame-Options "SAMEORIGIN" always;
  add_header X-XSS-Protection "1; mode=block" always;
  add_header X-Robots-Tag none always;
  add_header X-Download-Options noopen always;
  add_header X-Permitted-Cross-Domain-Policies none always;

  location = /robots.txt {
    allow all;
    log_not_found off;
    access_log off;
  }
  location = /.well-known/carddav {
    return 301 $scheme://$host/remote.php/dav;
  }
  location = /.well-known/caldav {
    return 301 $scheme://$host/remote.php/dav;
  }

  # set max upload size
  client_max_body_size 512M;
  fastcgi_buffers 8 4K;                     # Please see note 1
  fastcgi_ignore_headers X-Accel-Buffering; # Please see note 2

  # Disable gzip to avoid the removal of the ETag header
  # Enabling gzip would also make your server vulnerable to BREACH
  # if no additional measures are done. See https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=773332
  gzip off;

  # Uncomment if your server is build with the ngx_pagespeed module
  # This module is currently not supported.
  #pagespeed off;

  error_page 403 /core/templates/403.php;
  error_page 404 /core/templates/404.php;

  location / {
    rewrite ^ /index.php$uri;
  }

  location ~ ^/(?:build|tests|config|lib|3rdparty|templates|data)/ {
    return 404;
  }
  location ~ ^/(?:\.|autotest|occ|issue|indie|db_|console) {
    return 404;
  }

  location ~ ^/(?:index|remote|public|cron|core/ajax/update|status|ocs/v[12]|updater/.+|ocs-provider/.+|ocm-provider/.+|core/templates/40[34])\.php(?:$|/) {
    fastcgi_split_path_info ^(.+\.php)(/.*)$;
    include fastcgi_params;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    fastcgi_param SCRIPT_NAME $fastcgi_script_name; # necessary for owncloud to detect the contextroot https://github.com/owncloud/core/blob/v10.0.0/lib/private/AppFramework/Http/Request.php#L603
    fastcgi_param PATH_INFO $fastcgi_path_info;
    fastcgi_param HTTPS on;
    fastcgi_param modHeadersAvailable true; #Avoid sending the security headers twice
    fastcgi_param front_controller_active true;
    fastcgi_read_timeout 180; # increase default timeout e.g. for long running carddav/ caldav syncs with 1000+ entries
    fastcgi_pass php-handler;
    fastcgi_intercept_errors on;
    fastcgi_request_buffering off; #Available since NGINX 1.7.11
  }

  location ~ ^/(?:updater|ocs-provider|ocm-provider)(?:$|/) {
    try_files $uri $uri/ =404;
    index index.php;
  }

  # Adding the cache control header for js and css files
  # Make sure it is BELOW the PHP block
  location ~ \.(?:css|js)$ {
    try_files $uri /index.php$uri$is_args$args;
    add_header Cache-Control "max-age=15778463" always;

    # Add headers to serve security related headers (It is intended to have those duplicated to the ones above)
    # The always parameter ensures that the header is set for all responses, including internally generated error responses.
    # Before enabling Strict-Transport-Security headers please read into this topic first.
    # https://www.nginx.com/blog/http-strict-transport-security-hsts-and-nginx/

    #add_header Strict-Transport-Security "max-age=15552000; includeSubDomains; preload" always;
    add_header X-Content-Type-Options nosniff always;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Robots-Tag none always;
    add_header X-Download-Options noopen always;
    add_header X-Permitted-Cross-Domain-Policies none always;
    # Optional: Don't log access to assets
    access_log off;
  }

  location ~ \.(?:svg|gif|png|html|ttf|woff|ico|jpg|jpeg|map|json)$ {
    add_header Cache-Control "public, max-age=7200" always;
    try_files $uri /index.php$uri$is_args$args;
    # Optional: Don't log access to other assets
    access_log off;
  }

}
```
