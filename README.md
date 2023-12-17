# Keel Multi-Arch Image Builder

## Synopsis

Currently, there are [no official up-to-date](https://hub.docker.com/r/keelhq/keel-arm) arm64 Docker images available for [Keel](https://keel.sh). That makes it challenging to run Keel on aarch64 machines. This repository contains an [automated workflow](https://github.com/fardjad/keel-multi-arch/blob/main/.github/workflows/build-and-push.yml) that checks for new releases of Keel every day. Upon detecting a new release, the workflow builds a multi-architecture Docker image for both amd64 and arm64 architectures and pushes it to DockerHub under the repository [fardjad/keel](https://hub.docker.com/repository/docker/fardjad/keel).

## Usage with the Official Helm Chart

You can use this image with the official Helm chart by overriding the `image.repository` value:

```bash
helm repo add keel https://charts.keel.sh
helm repo update
helm upgrade --install \
    keel keel/keel \
    --namespace=kube-system \
    --set helmProvider.version="v3" \
    --set image.repository=fardjad/keel
```
