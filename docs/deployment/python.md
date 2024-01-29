---
icon: material/language-python
---

# Python

ExaCheck requires a recent version of Python; **Python 3.11 or higher is required**. For best results Python 3.12 is recommended. If you try to run ExaCheck on an earlier release of Python it will not work.

## PyPI Package

ExaCheck can be installed using `pip` from the [PyPI package repository][ExaCheck PyPI Package Repository]:

```bash
python3 -m pip install exacheck
```

All requirements will be installed automatically.

After installation you may configure ExaCheck using one of the [example configuration files][ExaCheck Examples] as a template.

## Python Modules

Various Python modules are required to use ExaCheck. The current requirements and their versions can be found in the [pyproject.toml file][ExaCheck PyProject].

### Main Script

These dependencies are used as a part of the main script.

- [Apprise][Apprise]: `apprise` is used to handle notifications to external services.
- [ExaBGP][ExaBGP]: `exabgp` is used to actually talk BGP; ExaCheck communicates with ExaBGP to announce or withdraw routes as needed.
- [Loguru][Loguru]: `loguru` is used for logging.
- [Pydantic][Pydantic]: `pydantic` is used to validate and store the configuration objects and check results.
- [PyYAML][PyYAML]: `pyyaml` is used to load and parse the configuration file into a dict, ready for [Pydantic][Pydantic] to consume.
- [setproctitle][setproctitle]: `setproctitle` will change the process title for the child processes.
- [tabulate][tabulate]: `tabulate` is used to format output into a table.
- [UltraJSON][UltraJSON]: `ujson` is used for loading configuration from JSON.

### Health Checks

These dependencies are required for the various health checks to work.

- [dnspython][dnspython]: `dnspython` is used for the `dns` health check method and to look up hostnames when required for other checks.
- [requests][requests]: `requests` is used for the `http` health check method.
- [icmplib][icmplib]: `icmplib` is used for the `icmp` health check method.
- [ntplib][ntplib]: `ntplib` is used for the `ntp` health check method.

### Command Line Interface

These dependencies are required for the command line interface.

- [Click][Click]: `click` provides the command line interface.

### Sentry

If you would like to enable [Sentry][Sentry] support, the `sentry-sdk` module must be installed.

### icmplib Note

By default, [icmplib][icmplib] is used in non-privileged mode. There **ARE** some requirements for this to work depending on the Linux distribution, see step 2 on the [icmplib without privileges][icmplib without privileges] page.

[Click]: https://click.palletsprojects.com/
[dnspython]: https://www.dnspython.org/
[ExaBGP]: https://github.com/Exa-Networks/exabgp
[ExaCheck PyProject]: https://github.com/exacheck/exacheck/blob/main/pyproject.toml
[icmplib without privileges]: https://github.com/ValentinBELYN/icmplib/blob/main/docs/6-use-icmplib-without-privileges.md
[icmplib]: https://github.com/ValentinBELYN/icmplib
[Loguru]: https://github.com/Delgan/loguru
[ntplib]: https://github.com/cf-natali/ntplib
[Pydantic]: https://docs.pydantic.dev/
[PyYAML]: https://pyyaml.org/
[requests]: https://requests.readthedocs.io/en/latest/
[setproctitle]: https://github.com/dvarrazzo/py-setproctitle
[tabulate]: https://github.com/astanin/python-tabulate
[UltraJSON]: https://github.com/ultrajson/ultrajson
[Apprise]: https://github.com/caronc/apprise
[Sentry]: https://sentry.io/welcome/
[ExaCheck PyPI Package Repository]: https://pypi.org/project/exacheck/
[ExaCheck Examples]: examples.md
