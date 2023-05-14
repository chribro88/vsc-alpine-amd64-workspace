# Alpine VS Code Remote Development Container 
 - with Miniconda & Docker
 - Alpine 3.18

Build and commit following first:
1. https://github.com/chribro88/docker-alpine-glibc

```
docker build --build-arg BASE_VERSION=3.18 https://github.com/chribro88/docker-alpine-glibc.git -t [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>]
```

2. https://github.com/chribro88/docker-alpine-miniconda3
```
docker build --build-arg IMAGE=[<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>] https://github.com/chribro88/docker-alpine-miniconda3.git -t [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
```

3. Update `devcontainer.json`, `settings.json` and `Dockerfile`:
   - devcontainer.json
     - LOCAL_USERNAME
     - PATH
     - REGISTRY_HOST
     - REGISTRY_USERNAME
   - settings.json
     - DOCKER_HOST
   - Dockerfile
     - DOCKER_GID

4. Pull the image to local docker host, then reopening container in vscode
```
docker pull  [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
```
