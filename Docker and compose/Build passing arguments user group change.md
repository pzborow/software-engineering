# Build passing arguments user group change

`docker-compose build --build-arg DOCKER_UID=1001 --build-arg DOCKER_GID=1001`

In docker file insert
```dockerfile
# in local dev, passing your host uid/gid will be helpful
ARG DOCKER_UID=1000
ARG DOCKER_GID=1000
RUN groupadd -g ${DOCKER_GID} django && useradd -u ${DOCKER_UID} -g django django
```