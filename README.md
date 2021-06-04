# docker-voublazars

Docker container for [VOU-Blazars](https://github.com/ecylchang/VOU_Blazars)


## Update image to a specific VOU_Blazars git repo tag

```bash
$ cd dockerfile/
$ TAG="1.94"
$ docker build -t my_voublazars --build-arg $TAG -f Dockerfile.update .
```


## Build image

```bash
$ cd docker-voublazars/
$ docker build --no-cache -t voub:test dockerfile/
```


## Run container
Check the docs in the DockerHub page: https://hub.docker.com/r/chbrandt/voublazars
