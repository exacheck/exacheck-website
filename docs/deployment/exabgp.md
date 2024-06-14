---
icon: material/router
description: Configuration information for ExaBGP to implement ExaCheck.
---

# ExaBGP

If installing ExaCheck from PyPi or source, ExaBGP requires some additional setup steps. If you are deploying the Docker container there is no need to follow the below steps.

!!! warning
    If using Python 3.12 and installing an older ExaBGP release, you may get the following error when running ExaBGP:

    ```bash
    root@970372c5ffcd:/# exabgp
    Traceback (most recent call last):
    File "/usr/local/bin/exabgp", line 8, in <module>
        sys.exit(run_exabgp())
                ^^^^^^^^^^^^
    File "/usr/local/lib/python3.12/site-packages/exabgp/application/__init__.py", line 18, in run_exabgp
        from exabgp.application.bgp import main
    File "/usr/local/lib/python3.12/site-packages/exabgp/application/bgp.py", line 18, in <module>
        from exabgp.logger import Logger
    File "/usr/local/lib/python3.12/site-packages/exabgp/logger.py", line 23, in <module>
        from exabgp.configuration.environment import environment
    File "/usr/local/lib/python3.12/site-packages/exabgp/configuration/environment.py", line 318, in <module>
        from exabgp.vendoring.six.moves import configparser as ConfigParser
    ModuleNotFoundError: No module named 'exabgp.vendoring.six.moves'
    ```

    If you encounter this error, ExaBGP must be installed from source rather than the current PyPi release. Make sure `git` is available and install from the GitHub repository instead:

    ```bash
    python3 -m pip install git+https://github.com/Exa-Networks/exabgp.git@4.2
    ```

## System User

A user account should be added for ExaBGP so it does not run as root. To add the account:

```bash
useradd -Ms /usr/sbin/nologin -d /run/exabgp exabgp
```

## systemd Service File

Installing ExaBGP from source or pip does not include a systemd service file. Create the file `/etc/systemd/system/exabgp.service` with this content:

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

## Configuration

ExaBGP needs to be configured to use ExaCheck. By default, the ExaBGP and ExaCheck configuration will be sourced from the `/etc/exabgp` directory; create that directory if it does not already exist:

```bash
mkdir /etc/exabgp
```

### Environment File

The ExaBGP environment file needs to be created. To generate a default environment file run the following command:

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

### Configuration File

The ExaBGP configuration file, `/etc/exabgp/exabgp.conf`, then needs to be created. An example template:

```c
# Define the ExaCheck process
process exacheck {
    run exacheck run;
    encoder text;
}

# Connect to the BGP neighbor 192.0.2.1
neighbor 192.0.2.1 {
    description "Example BGP neighbor";

    # This should be set to the ExaBGP router ID (eg. the main IP address of this server)
    router-id 192.0.2.10;

    # The local address to source BGP connections from
    local-address 192.0.2.10;

    # The local and peer AS numbers
    local-as 65515;
    peer-as 65515;

    # The address family to advertise
    family {
        ipv4 unicast;
    }

    # Allow routes sent from the ExaCheck process to be sent to this neighbor
    api {
        processes [ exacheck ];
    }
}
```

For more configuration examples, see the [ExaCheck configuration examples page][ExaCheck Examples].

Once ExaBGP and ExaCheck have been configured, the systemd service can then be started:

```bash
systemctl start exabgp.service
```

[ExaCheck Examples]: examples.md
