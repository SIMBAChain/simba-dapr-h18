# dapr v1.13.5

## Pre-requisites
Install go version v1.23.0 as per the [installation documentation](https://go.dev/doc/install).

## Build container images
Run the following sequence of command to build the container images using docker:
```bash
go clean -modcache
make modtidy-all
make
DAPR_REGISTRY=registry.gitlab.com/simbachain/images/dapr DAPR_TAG=1.13.5.patch.0 make docker-build
```
If successful, six dapr container images will be created. Confirm the existence of these images by running
`docker images | grep dapr` which should produce the following output:
```
registry.gitlab.com/simbachain/images/dapr/injector      1.13.5.patch.0-linux-amd64   56badbc48949   2 days ago     43.5MB
registry.gitlab.com/simbachain/images/dapr/operator      1.13.5.patch.0-linux-amd64   001c30d3b807   2 days ago     44.3MB
registry.gitlab.com/simbachain/images/dapr/sentry        1.13.5.patch.0-linux-amd64   f0d8cac3af4c   2 days ago     45MB
registry.gitlab.com/simbachain/images/dapr/placement     1.13.5.patch.0-linux-amd64   817e1e5073c8   2 days ago     39MB
registry.gitlab.com/simbachain/images/dapr/daprd         1.13.5.patch.0-linux-amd64   e24ea1672946   2 days ago     184MB
registry.gitlab.com/simbachain/images/dapr/dapr          1.13.5.patch.0-linux-amd64   dc803bf4c908   2 days ago     348MB
```

## Publish container images
First rename the container images by dropping the `-linux-amd64` tag suffix:
```bash
docker tag registry.gitlab.com/simbachain/images/dapr/injector:1.13.5.patch.0-linux-amd64 registry.gitlab.com/simbachain/images/dapr/injector:1.13.5.patch.0
docker tag registry.gitlab.com/simbachain/images/dapr/operator:1.13.5.patch.0-linux-amd64 registry.gitlab.com/simbachain/images/dapr/operator:1.13.5.patch.0
docker tag registry.gitlab.com/simbachain/images/dapr/sentry:1.13.5.patch.0-linux-amd64 registry.gitlab.com/simbachain/images/dapr/sentry:1.13.5.patch.0
docker tag registry.gitlab.com/simbachain/images/dapr/placement:1.13.5.patch.0-linux-amd64 registry.gitlab.com/simbachain/images/placement/dapr:1.13.5.patch.0
docker tag registry.gitlab.com/simbachain/images/dapr/daprd:1.13.5.patch.0-linux-amd64 registry.gitlab.com/simbachain/images/dapr/daprd:1.13.5.patch.0
docker tag registry.gitlab.com/simbachain/images/dapr/dapr:1.13.5.patch.0-linux-amd64 registry.gitlab.com/simbachain/images/dapr/dapr:1.13.5.patch.0
```
Publish the container images to the registry:
```bash
docker push registry.gitlab.com/simbachain/images/dapr/injector:1.13.5.patch.0
docker push registry.gitlab.com/simbachain/images/dapr/operator:1.13.5.patch.0
docker push registry.gitlab.com/simbachain/images/dapr/sentry:1.13.5.patch.0
docker push registry.gitlab.com/simbachain/images/dapr/placement:1.13.5.patch.0
docker push registry.gitlab.com/simbachain/images/dapr/daprd:1.13.5.patch.0
docker push registry.gitlab.com/simbachain/images/dapr/dapr:1.13.5.patch.0
```
