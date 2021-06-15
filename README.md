# docker-compose
All sorts of docker-compose recipes for deploying Chevereto

# How-to

For now, just per-folder structure. ie:

- /portainer
- /unraid
- /owner
- /etc

# Httpd version `docker-compose` guide

Firstly, to install docker and docker-compose on your host machine, follow these official guides:

[Docker](https://docs.docker.com/get-docker/)
[docker-compose](https://docs.docker.com/compose/install/)

As long as you installed the Docker and docker-compose, clone this repo:

```bash
git clone https://github.com/Chevereto/docker-compose.git
```

Then, you need to config your application with environment variables (all variables were listed in [Chevereto/docker](https://github.com/Chevereto/docker#readme)) in `conf.env`.

Now, you can start your service:

```bash
docker-compose up -d
```

# Config a Nginx reverse proxy

You can use Nginx reverse proxy to serve your site, a sample config block as below:

```nginx
server {
  listen 80;
  listen [::]:80;
  server_name example.com;

  client_max_body_size 100m;

  location / {
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-NginX-Proxy true;
    proxy_pass http://127.0.0.1:8000/;
    proxy_redirect off;
  }
}
```
