---
title: Home
layout: home
---

# ExaCheck - ExaBGP Health Checker

[ExaCheck][ExaCheck GitHub Project] works in conjunction with [ExaBGP] to health check services and announce BGP routes based on the availability of those services.

There are various other health checking projects for ExaBGP including one [included with ExaBGP][ExaBGP Healthcheck] how ever ExaCheck differs in multiple ways to suite my environment.

## Why ExaCheck

[ExaBGP] is packaged with its own health checking script ([see here][ExaBGP Healthcheck]) however it has some limitations which make it not suitable for my requirements. The built in health check works fine for smaller environments where each service may be running its own instance of ExaBGP (so each instance of ExaBGP runs one or only a few processes) however for larger environments where health checks are centralized it becomes unmanageable.

Some features from the built in ExaBGP health checking script are **not** available as they are not relevant to the use case for me:

- Management of IP address binding; the main use case of ExaCheck is for centralized health checks where the service resides on another server/container/VM

[ExaCheck GitHub Project]: https://github.com/exacheck/exacheck
[ExaBGP]: https://github.com/Exa-Networks/exabgp
[ExaBGP Healthcheck]: https://github.com/Exa-Networks/exabgp/blob/main/src/exabgp/application/healthcheck.py