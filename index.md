---
title: Home
description: ExaCheck - Health check services and advertise BGP routes using ExaBGP.
layout: home
nav_order: 1
permalink: /
---

# ExaCheck - ExaBGP Health Checker

Health check services and advertise BGP routes using ExaBGP.
{: .fs-6 .fw-300 }

[Get ExaCheck][ExaCheck]{: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

----

[ExaCheck] works in conjunction with [ExaBGP] to health check services and announce BGP routes based on the availability of those services.

ExaCheck is configured in a YAML based configuration file ([example][ExaCheck Sample Configuration]) which allows for easy configuration of health checks without having to create scripts.

## Why ExaCheck

ExaBGP is packaged with its own health checking script ([see here][ExaBGP Healthcheck]) however it has some limitations which make it not suitable for my requirements.

The built in health check works fine for smaller environments where each service may be running its own instance of ExaBGP (so each instance of ExaBGP runs one or only a few processes) however for larger environments where health checks are centralized it becomes unmanageable.

## Features

- Live configuration reloads (adding/modifying/removing services)
- Health checks implemented in pure python where possible; no need to write scripts or use chains of commands to validate output
- Detailed logging available
- Configuration validation (if using live configuration reloads, configuration is validated before application)
- Out of the box sane defaults where possible
- Choice of thread or process based health checks
- JSON schema of configuration (see [configuration.json][ExaCheck Configuration Schema] for the current schema)
- Easy Docker deployment (see [docker-compose.yaml][ExaCheck docker-compose.yaml] for an example)

[ExaCheck]: https://github.com/exacheck/exacheck
[ExaCheck docker-compose.yaml]: https://github.com/exacheck/exacheck/blob/main/docker-compose.yaml
[ExaCheck Sample Configuration]: https://github.com/exacheck/exacheck/blob/main/configuration.yaml
[ExaCheck Configuration Schema]: https://github.com/exacheck/exacheck/blob/main/configuration.json
[ExaBGP]: https://github.com/Exa-Networks/exabgp
[ExaBGP Healthcheck]: https://github.com/Exa-Networks/exabgp/blob/main/src/exabgp/application/healthcheck.py