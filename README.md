# docker-voublazars

Docker container for [VOU-Blazars](https://github.com/ecylchang/VOU_Blazars)


## Update image to a specific VOU_Blazars git repo tag

```bash
$ cd dockerfile/
$ docker build -t chbrandt/voublazars:1.98 --build-arg TAG="v1.98" -f Dockerfile.update .
```


## Build image

```bash
$ cd docker-voublazars/
$ docker build --no-cache -t voub:test dockerfile/
```


## Run container
Check the docs in the DockerHub page: https://hub.docker.com/r/chbrandt/voublazars
