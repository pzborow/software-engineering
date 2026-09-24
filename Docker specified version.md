# Docker specified version

Spradzenie dostępnych wersji
` apt-cache policy docker-ce`

Następnie po wybraniu właściwej
```
DOCKER_VERSION=5:20.10.23~3-0~ubuntu-bionic
sudo apt-get install docker-ce=$DOCKER_VERSION docker-ce-cli=$DOCKER_VERSION containerd.io docker-buildx-plugin docker-compose-plugin
```