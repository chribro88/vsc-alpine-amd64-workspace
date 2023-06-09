# Alpine VS Code Remote Development Container 
 - with Miniconda & Docker
 - Alpine 3.18

1. Build alpine-glibc:
    - https://github.com/chribro88/docker-alpine-glibc

```
docker build --build-arg BASE_VERSION=3.18 https://github.com/chribro88/docker-alpine-glibc.git -t [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>]

# optional - tag and send to local registry
docker tag alpine-glibc[:<BASE_VERSION>] [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>]
docker push  [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>]

```
2. Build alpine-miniconda3:
    - https://github.com/chribro88/docker-alpine-miniconda3
```
docker build --build-arg IMAGE=[<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>] https://github.com/chribro88/docker-alpine-miniconda3.git -t [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]

# optional - tag and send to local registry
docker tag alpine-miniconda3[:<BASE_VERSION>] [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
docker push  [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
```

3. Update `devcontainer.json`, `settings.json` and `Dockerfile`:
   - devcontainer.json
     - LOCAL_USERNAME
     - PATH
     - REGISTRY_HOST
     - REGISTRY_USERNAME
     - BASE_VERSION
   - settings.json
     - DOCKER_HOST
   - Dockerfile
     - DOCKER_GID

4. Reopen container in vscode (Need image on local docker host so pull if not)
```
docker pull  [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
```

# Credits
Adapted from the following:
- https://github.com/Docker-Hub-frolvlad/docker-alpine-glibc
- https://github.com/Docker-Hub-frolvlad/docker-alpine-miniconda3
- https://github.com/senglin/python-rpi4-workspace
