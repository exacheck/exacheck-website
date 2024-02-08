---
icon: material/docker
---

# Docker

A pre-built image of ExaCheck including the various requirements is available from the [ExaCheck Docker Hub page][ExaCheck Docker Hub]. To use the image you will need to create the `exabgp.conf` and `exacheck.yaml` configuration files.

## Docker Compose

A [Docker Compose file][ExaCheck Docker Compose File] is available. Included in the repository is a [sample ExaBGP configuration file][ExaBGP Example Configuration File] and [sample ExaCheck configuration file][ExaCheck Example Configuration File].

## Inbound Connections

By default, ExaBGP does not listen for inbound BGP connections; only outbound connections are established. To allow inbound connections the environment variable `exabgp.tcp.bind` needs to be set. The provided Docker compose file does not allow inbound connections by default - the relevant environment line can be uncommented if you want to allow them.

## Customising ExaCheck/Python Release

The [Dockerfile][ExaCheck Dockerfile] is available should you want to change Python and/or ExaCheck release. The following build arguments are supported:

* `PYTHON_VERSION`: The Python version for the container. Defaults to `3.11` currently.
* `EXACHECK_VERSION`: The ExaCheck branch or tag to build from. Defaults to `v0.0.10` currently.
* `EXACHECK_REPOSITORY`: The ExaCheck repository URL to clone from. Defaults to `https://github.com/exacheck/exacheck.git`.

The same Dockerfile is used for building the DockerHub images.

[ExaCheck Docker Compose File]: https://github.com/exacheck/exacheck/blob/main/docker/docker-compose.yaml
[ExaCheck Dockerfile]: https://github.com/exacheck/exacheck/blob/main/docker/Dockerfile
[ExaBGP Example Configuration File]: https://github.com/exacheck/exacheck/blob/main/docker/exabgp.conf
[ExaCheck Example Configuration File]: https://github.com/exacheck/exacheck/blob/main/docker/exacheck.yaml
[ExaCheck Docker Hub]: https://hub.docker.com/r/exacheck/exacheck
