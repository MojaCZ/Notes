https://www.domysee.com/blogposts/reverse-proxy-nginx-docker-compose

# Dockerfile



# docker-compose.yml
version:
services: 
  image:
  container_name:
  volumes:
    * defines the persistent storage for docker containers
    * if application writes somewhere no volumes is defined, that data will be last when container stops
    * map specific file or directorz into the container `- ./nginx.conf:/etc/nginx/nginx.conf`
    * named volumes can be specified similar to networks in root entry `volumes: ` `- "someVolume:/etc/something"`
  ports:
  networks:
    * specifies which container can talk to each other
    * I can then refers to container by name `http://serviceName`
  expose:
  environment:
    * environment variables for the application in container
    * !!! overrides once in files
    * `- ENV=development`
    * `- APPLICATION_URL=http://somepath`

networks:
volumes:


# Nginx
```conf
http {
  server {
    server_name your.server.url;

    location /yourService1 {
      proxy_pass http://localhost:80;
      rewrite ^/yourService1(.*)$ $1 break;
    }

    location /yourService2 {
      proxy_pass http://localhost:5000;
      rewrite ^/yourService1(.*)$ $1 break;
    }
  }

  server {
    server_name another.server.url;

    location /yourService1 {
      proxy_pass http://localhost:80;
      rewrite ^/yourService1(.*)$ $1 break;
    }

    location /yourService3 {
      proxy_pass http://localhost:5001;
      rewrite ^/yourService1(.*)$ $1 break;
    }
  }
}
```

`server` 
  * configuration specifies a virtual server, where each can have its own rules.
  * The server_name defines which urls or IP addresses virtual server responds to.
`location`
  * defines where to route incoming traffic
  * `proxy_pass` sets the new url, with `rewrite` the url is rewritten so that it fits the service (`rewrite ^/myService(.*)$ $1 break;` will remove myService from url)


# Nginx inside Docker



image - is binaries, libraries and sourcecode that runs the application
container - running instance of that image

`docker container run --publish 80:80 nginx` will look for an image called nginx, pull down latest image and start it, it also relocate from port 80 to port 80
`docker container run --publish 80:80 --detach nginx` --detach will tell docker to run it on background
`docker container run --publish 80:80 --detach --name webhost nginx` will also create name for container (normally it is generated randomly)

`docker container ls` will list all running containers
`docker container ls -a`
`docker container stop 390` will stop container with id starting with 390 (it is easier, ids are long)

`docker container logs webhost` will show logs of webhost container

`docker container rm 35d`
`docker container rm -f 35d` will force removing container

`docker ps`

NGINX
`docker run --name mynginx -P -d nginx`



DOCKER ON SERVER
mkdir dockerbuild - configuration will be here
nano Dockerfile
docker build -t "webdev:Dockerfile" .

Dockerfile
```bash
FROM ubuntu:18.04
LABEL maintainer="NGINX Docker Mintainers <docker-maint@nginx.com>"

# Download certificate and key from the customer portal (https://cs.nginx.com)
# and copy to the build context
COPY nginx-repo.crt /etc/ssl/nginx/
COPY nginx-repo.key /etc/ssl/nginx/

# Install NGINX Plus
RUN set -x \
  && apt-get update && apt-get upgrade -y \
  && apt-get install --no-install-recommends --no-install-suggests -y apt-transport-https ca-certificates gnupg1 \
  && \
  NGINX_GPGKEY=573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62; \
  found=''; \
  for server in \
    ha.pool.sks-keyservers.net \
    hkp://keyserver.ubuntu.com:80 \
    hkp://p80.pool.sks-keyservers.net:80 \
    pgp.mit.edu \
  ; do \
    echo "Fetching GPG key $NGINX_GPGKEY from $server"; \
    apt-key adv --keyserver "$server" --keyserver-options timeout=10 --recv-keys     "$NGINX_GPGKEY" && found=yes && break; \
  done; \
  test -z "$found" && echo >&2 "error: failed to fetch GPG key $NGINX_GPGKEY" && exit 1; \
  echo "Acquire::https::plus-pkgs.nginx.com::Verify-Peer \"true\";" >> /etc/apt/apt.conf.d/90nginx \
  && echo "Acquire::https::plus-pkgs.nginx.com::Verify-Host \"true\";" >> /etc/apt/apt.conf.d/90nginx \
  && echo "Acquire::https::plus-pkgs.nginx.com::SslCert     \"/etc/ssl/nginx/nginx-repo.crt\";" >> /etc/apt/apt.conf.d/90nginx \
  && echo "Acquire::https::plus-pkgs.nginx.com::SslKey      \"/etc/ssl/nginx/nginx-repo.key\";" >> /etc/apt/apt.conf.d/90nginx \
  && printf "deb https://plus-pkgs.nginx.com/debian stretch nginx-plus\n" > /etc/apt/sources.list.d/nginx-plus.list \
  && apt-get update && apt-get install -y nginx-plus \
  && apt-get remove --purge --auto-remove -y gnupg1 \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /etc/ssl/nginx

# Forward request logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
&& ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80

STOPSIGNAL SIGTERM

CMD "nginx", "-g", "daemon off;"
```