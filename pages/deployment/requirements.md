---
title: Requirements
description: Minimum requirements to run ExaCheck.
layout: page
nav_order: 0
permalink: /deployment/requirements.html
parent: Deployment
---

# ExaCheck Requirements
{: .no_toc }

The minimum requirements needed to run ExaCheck in your environment. The recommended deployment method is Docker; see the [Docker steps here][ExaCheck Docker Deployment].

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Python

ExaCheck requires a recent version of Python; Python 3.10 or higher is required. If you try to run ExaCheck on an earlier release of Python it will not work.

## Python Modules

Various Python modules are required to use ExaCheck. The current requirements and their versions can be found in the [pyproject.toml file][ExaCheck PyProject].

### Main Script

These dependencies are used as a part of the main script.

- [ExaBGP][ExaBGP]: `exabgp` is used to actually talk BGP; ExaCheck communicates with ExaBGP to announce or withdraw routes as needed.
- [Loguru][Loguru]: `loguru` is used for logging.
- [Pydantic][Pydantic]: `pydantic` is used to validate and store the configuration objects and check results.
- [PyYAML][PyYAML]: `pyyaml` is used to load and parse the configuration file into a dict, ready for [Pydantic][Pydantic] to consume.
- [setproctitle][setproctitle]: `setproctitle` will change the process title for the child processes (when ExaCheck is running in `processes` mode).
- [tabulate][tabulate]: `tabulate` is used to format output into a table.

### Health Checks

These dependencies are required for the various health checks to work.

- [dnspython][dnspython]: `dnspython` is used for the `dns` health check method.
- [httpx][httpx]: `httpx` is used for the `http` health check method.
- [icmplib][icmplib]: `icmplib` is used for the `icmp` health check method.
- [ntplib][ntplib]: `ntplib` is used for the `ntp` health check method.
- [pyrad][pyrad]: `pyrad` is used for the `radius` health check method.
- [python-ldap][python-ldap]: `python-ldap` is used for the `ldap` health check method.

### Command Line Interface

These dependencies are required for the command line interface.

- [Click][Click]: `click` provides the command line interface.

## OS Requirements

There are no specific OS/distribution requirements.

### icmplib Note

By default, [icmplib][icmplib] is used in non-privileged mode. There **ARE** some requirements for this to work depending on the Linux distribution, see step 2 on the [icmplib without privileges][icmplib without privileges] page.

[Click]: https://click.palletsprojects.com/
[dnspython]: https://www.dnspython.org/
[ExaBGP]: https://github.com/Exa-Networks/exabgp
[ExaCheck Docker Deployment]: /deployment/docker.html
[ExaCheck PyProject]: https://github.com/exacheck/exacheck/blob/main/pyproject.toml
[httpx]: https://www.python-httpx.org/
[icmplib without privileges]: https://github.com/ValentinBELYN/icmplib/blob/main/docs/6-use-icmplib-without-privileges.md
[icmplib]: https://github.com/ValentinBELYN/icmplib
[Loguru]: https://github.com/Delgan/loguru
[ntplib]: https://github.com/cf-natali/ntplib
[Pydantic]: https://docs.pydantic.dev/
[pyrad]: https://github.com/pyradius/pyrad
[python-ldap]: https://www.python-ldap.org
[PyYAML]: https://pyyaml.org/
[setproctitle]: https://github.com/dvarrazzo/py-setproctitle
[tabulate]: https://github.com/astanin/python-tabulate
