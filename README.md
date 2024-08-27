[![Docker Image CI](https://github.com/f1d094/alarmdecoder-webapp-docker/actions/workflows/docker-image.yml/badge.svg)](https://github.com/f1d094/alarmdecoder-webapp-docker/actions/workflows/docker-image.yml)

# AlarmDecoder Webapp Dockerfile

This is a Dockerfile for the [AlarmDecoder Webapp](https://github.com/nutechsoftware/alarmdecoder-webapp) project. It is built by following the build instructions in that project's README, with a few tweaks to adapt to the Docker environment.

## Run Container

The container is available pre-built on [Docker Hub](https://hub.docker.com/r/f1d094/alarmdecoder-webapp-docker/).

```
podman run -d \
  --name alarmdecoder-webapp \
  --privileged \
  --restart=unless-stopped \
  -v /etc/localtime:/etc/localtime:ro \
  -p 127.0.0.1:5000:5000 \
  --device /dev:/dev \
  f1d094/alarmdecoder-webapp-docker
```

You can then access AlarmDecoder at `http://localhost:5000`. If you want to run this on a remote host it is recommended to use ssh tunnel ssh -L 5000:127.0.0.1:5000 <remotehost>

## Complete Setup

This container exposes the gunicorn workers directly, it's recommended that set
up an nginx reverse proxy in front of the app.

You'll also likely want to created a named or mounted volume to persist the
configuration and logging, which lives at `/opt/alarmdecoder-webapp/instance`.

