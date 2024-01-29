---
icon: material/docker
---

# Docker

A pre-built image of ExaCheck including the various requirements is available from the [ExaCheck Docker Hub page][ExaCheck Docker Hub]. To use the image you will need to create the `exabgp.conf` and `exacheck.yaml` configuration files.

## Docker Compose

A [Docker Compose file][ExaCheck Docker Compose File] is available. Included in the repository is a [sample ExaBGP configuration file][ExaBGP Example Configuration File] and [sample ExaCheck configuration file][ExaCheck Example Configuration File].

[ExaCheck Docker Compose File]: https://github.com/exacheck/exacheck/blob/main/docker/docker-compose.yaml
[ExaBGP Example Configuration File]: https://github.com/exacheck/exacheck/blob/main/docker/exabgp.conf
[ExaCheck Example Configuration File]: https://github.com/exacheck/exacheck/blob/main/docker/exacheck.yaml
[ExaCheck Docker Hub]: https://hub.docker.com/r/exacheck/exacheck
