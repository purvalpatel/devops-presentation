Why Docker-compose ?
-------------------
Running multiple apps using `docker run` will be messy. like application, database, logger, caching etc.
Docker Compose lets you define and run multi-container apps using a single YAML file.

1. Manage multiple containers easily
2. Define everything in one YAML file
3. Portable & reproducible setup
4. One command to start/stop everything

installation:
---------------
```
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v2.38.2/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose

chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

mv $DOCKER_CONFIG/docker-compose /usr/local/bin/
```
check version:
```
docker-compose --version
```

Sample code for docker-compose:
------------------------------

docker-compose.yaml
```YAML
version: "3.8"

services:
  web:
    image: python:3.10-slim
    container_name: my_web
    command: python -m http.server 8000
    ports:
      - "8000:8000"

  redis:
    image: redis:alpine
    container_name: my_redis

```
Run the containers:
```
docker-compose up -d
```

Start/Stop containers:
```
docker-compose stop
docker-compose start
docker-compose restart
docker-compose down
```
