# DockerCache

This image makes the docker registry default to "proxy" mode, which means you can cache docker images locally.

The proxy is insecure, meaning it does not require any credentials to connect to it. It simply acts as a proxy between your docker daemon and docker hub.

# Installation

```
docker run -d -p 5000:5000 --restart=always --name registry -v ~/data:/var/lib/registry philwinder/dockercache
```

This command will save the registry data to the `~/data` directory. It also sets restart to `always`, which should mean it restarts whenever the docker daemon is shut down.

## Docker for mac

If using docker-for-mac, go to "Preferences"->"Advanced" and to the "Registry mirrors". Add a mirror named `http://localhost:5000`. It won't work without the http prefix.

## Others

If using another distribution, set the `--registry-mirrors` daemon option to `http://localhost:5000`

# Usage

To use, simply docker pull as usual. The image will be cached in your local repository. For example:

```
# time docker pull node:latest
...
Status: Downloaded newer image for node:latest
docker pull node:latest  0.13s user 0.09s system 0% cpu 3:33.13 total
# docker rmi node:latest
Untagged: node:latest
...
# time docker pull node:latest
...
Status: Downloaded newer image for node:latest
docker pull node:latest  0.12s user 0.08s system 0% cpu 24.302 total
```
