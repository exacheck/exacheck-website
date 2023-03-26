---
title: Home
description: ExaCheck - Health check services and advertise BGP routes using ExaBGP.
layout: home
nav_order: 0
permalink: /
---

# ExaCheck - ExaBGP Health Checker

Health check services and advertise BGP routes using ExaBGP.
{: .fs-6 .fw-300 }

[Features][ExaCheck Features]{: .btn .btn-blue .fs-5 .mb-4 .mb-md-0 .mr-2 } [Get ExaCheck][ExaCheck Deployment]{: .btn .btn-green .fs-5 .mb-4 .mb-md-0 .mr-2 }

----

[ExaCheck][ExaCheck GitHub] works in conjunction with [ExaBGP][ExaBGP GitHub] to health check services and announce BGP routes based on the availability of those services.

ExaCheck is configured in a YAML based configuration file ([example][ExaCheck Sample Configuration]) which allows for easy configuration of health checks without having to create scripts.

## Why ExaCheck

ExaBGP is packaged with its own health checking script ([see here][ExaBGP Healthcheck]) however it has some limitations which make it not suitable for my requirements.

The built in health check works fine for smaller environments where each service may be running its own instance of ExaBGP (so each instance of ExaBGP runs one or only a few processes) however for larger environments where health checks are centralized it becomes unmanageable.

[ExaCheck GitHub]: https://github.com/exacheck/exacheck
[ExaCheck Features]: /features.html
[ExaCheck Deployment]: /deployment.html
[ExaCheck Sample Configuration]: https://github.com/exacheck/exacheck/blob/main/configuration.yaml
[ExaBGP GitHub]: https://github.com/Exa-Networks/exabgp
[ExaBGP Healthcheck]: https://github.com/Exa-Networks/exabgp/blob/main/src/exabgp/application/healthcheck.py
