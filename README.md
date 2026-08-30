# Keel Multi-Arch Image Builder

<!-- prettier-ignore -->
> [!WARNING]
> This repository is no longer needed. Upstream Keel now provides
> official multi-architecture images for `linux/amd64` and `linux/arm64`: [PR
> #830][pr-830] added multi-architecture support, and [PR #906][pr-906]
> publishes those images to Docker Hub. Please use
> [`ghcr.io/keel-hq/keel`][keel-ghcr] or [`keelhq/keel`][keel-docker-hub]
> instead.

## Synopsis

Currently, there are [no official up-to-date][keel-arm-docker-hub] arm64 Docker
images available for [Keel][keel]. That makes it cumbersome to run Keel on
aarch64 machines. This repository contains an [automated
workflow][build-workflow] that checks for new releases of Keel every day. Upon
detecting a new release, the workflow builds a multi-architecture Docker image
for both amd64 and arm64 architectures and pushes it to DockerHub under the
repository [fardjad/keel][fardjad-keel-docker-hub].

## Usage with the Official Helm Chart

You can use this image with the official Helm chart by overriding the
`image.repository` value:

```bash
helm repo add keel https://charts.keel.sh
helm repo update
helm upgrade --install \
    keel keel/keel \
    --namespace=kube-system \
    --set helmProvider.version="v3" \
    --set image.repository=fardjad/keel
```

[pr-830]: https://github.com/keel-hq/keel/pull/830
[pr-906]: https://github.com/keel-hq/keel/pull/906
[keel-ghcr]: https://github.com/keel-hq/keel/pkgs/container/keel
[keel-docker-hub]: https://hub.docker.com/r/keelhq/keel
[keel-arm-docker-hub]: https://hub.docker.com/r/keelhq/keel-arm
[keel]: https://keel.sh
[build-workflow]:
  https://github.com/fardjad/keel-multi-arch/blob/main/.github/workflows/build-and-push.yml
[fardjad-keel-docker-hub]: https://hub.docker.com/repository/docker/fardjad/keel
