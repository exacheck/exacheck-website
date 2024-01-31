---
icon: material/language-python
---

# Python

ExaCheck requires a recent version of Python; **Python 3.11 is required**. If you try to run ExaCheck on an earlier release of Python it will not work. ExaBGP appears to have problems with Python 3.12; this page will be revised once a solution has been found.

## PyPI Package

ExaCheck can be installed using `pip` from the [PyPI package repository][ExaCheck PyPI Package Repository]:

```bash
python3 -m pip install exacheck
```

All requirements will be installed automatically.

After installation you may configure ExaCheck using one of the [example configuration files][ExaCheck Examples] as a template.

### venv

To install ExaCheck and ExaBGP in a Python virtual environment (in this example using `/opt/exacheck` as the root of the venv), follow the below steps:

1. Create the virtual environment:

```bash
python3 -m venv /opt/exacheck
```

2. Optionally, activate the environment:

```bash
source /opt/exacheck/bin/activate
```

3. Install the ExaCheck package:

```bash
/opt/exacheck/bin/python3 -m pip install exacheck
```

ExaCheck and ExaBGP are now ready to use.

## ExaBGP Setup Notes

If using PyPI to install ExaBGP a few extra steps should be performed.

### ExaBGP User

A user account should be added for ExaBGP so it does not run as root. To add the account:

```bash
useradd -Ms /usr/sbin/nologin -d /run/exabgp exabgp
```

### ExaBGP Service File

The pip install method of ExaBGP does not include a systemd service file. Create the file `/etc/systemd/system/exabgp.service` with this content:

```ini
[Unit]
Description=ExaBGP
Documentation=man:exabgp(1)
Documentation=man:exabgp.conf(5)
Documentation=https://github.com/Exa-Networks/exabgp/wiki
After=network.target
ConditionPathExists=/etc/exabgp/exabgp.conf

[Service]
Environment=exabgp_daemon_daemonize=false
User=exabgp
Group=exabgp
RuntimeDirectory=exabgp
RuntimeDirectoryMode=0750
ExecStartPre=-/usr/bin/mkfifo /run/exabgp/exabgp.in
ExecStartPre=-/usr/bin/mkfifo /run/exabgp/exabgp.out
ExecStart=/opt/exacheck/bin/exabgp /etc/exabgp/exabgp.conf
ExecReload=/bin/kill -USR1 $MAINPID
Restart=always
CapabilityBoundingSet=CAP_NET_ADMIN
AmbientCapabilities=CAP_NET_ADMIN

[Install]
WantedBy=multi-user.target
```

Once the service file is created the service can be enabled to start on boot:

```bash
systemctl enable exabgp.service
```

### ExaBGP Configuration

Create the ExaBGP and ExaCheck configuration files. By default they will be sourced from `/etc/exabgp`. The directory will need to be created:

```bash
mkdir /etc/exabgp
```

Create the default ExaBGP environment file:

```bash
/opt/exacheck/bin/exabgp --fi > /etc/exabgp/exabgp.env
```

The following configuration options need to be changed in the environment file:

- API `ack` set to `false`
- ExaBGP user changed from `nobody` to `exabgp`

A sed one liner to change the required values can be executed:

```bash
sed -i \
    -e "s:ack = true:ack = false:" \
    -e "s:user = 'nobody':user = 'exabgp':" \
    /etc/exabgp/exabgp.env
```

Once ExaBGP and ExaCheck has been configured (see the [configuration examples page][ExaCheck Examples]) the ExaBGP service can be started:

```bash
systemctl start exabgp.service
```

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
