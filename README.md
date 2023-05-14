# Alpine VS Code Remote Development Container 
 - with Miniconda & Docker
 - Alpine 3.18
 - 
Build and commit following first:
1. https://github.com/chribro88/docker-alpine-glibc

```
docker build \
  https://github.com/chribro88/docker-alpine-glibc#alpine-<BASE_VERSION> \
  -t [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-glibc[:<BASE_VERSION>]
```
2. https://github.com/chribro88/docker-alpine-miniconda3
```
docker build \
  https://github.com/chribro88/docker-alpine-miniconda3#alpine-<BASE_VERSION> \ 
  -t [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
```
3. Update `devcontainer.json` and `settings.json`:
 - LOCAL_USERNAME
 - PATH
 - REGISTRY_HOST
 - REGISTRY_USERNAME
 - DOCKER_HOST
5. Pull the image to local docker host, then reopening container in vscode
```
docker pull  [<REGISTRY_HOST>/][<REGISTRY_USERNAME>/]alpine-miniconda3[:<BASE_VERSION>]
```
