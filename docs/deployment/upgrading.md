---
icon: octicons/tracked-by-closed-completed-16
description: Upgrade steps and notes for ExaCheck installations using the PyPi packages or the ExaCheck Docker container.
---

# Upgrading

Upgrading ExaCheck depends on the initial installation method.

## Upgrade Process

If ExaCheck has been installed using `pip` (from PyPi or from source), the package can be upgraded by running the install command again with the `--upgrade` flag.

For the latest PyPi package:

```bash
python3 -m pip install exacheck --upgrade
```

If using the Docker image and the tag is set to `latest` (the default in the sample), simply pull and start:

```bash
docker compose pull
docker compose start
```

## Upgrade Notes

Every effort is made to keep the configuration file between releases compatible. From time to time there may be some configuration schema changes that must be made to add additional features or change how existing features work; these changes will be listed here.

### 0.0.6

When upgrading to `0.0.5`, the `monitoring_interval` and `live_reload` options have been migrated under the [`exacheck`][ExaCheck Configuration - Internal] configuration key.

### 0.1.7

The `0.1.7` release of ExaCheck introduces a dependency on ExaBGP v5. The new ExaBGP release introduces a slightly different command line. One of the changes that has impacted me has been the replacement of the `-e` flag for specifying an environment file with `--env-file`; I had a systemd service file that was using this `ExecStart` line:

```bash
ExecStart=/opt/exacheck/bin/exabgp -e /etc/exabgp/exabgp.env /etc/exabgp/exabgp.conf
```

The corrected line is (the addition of `server` is not required but recommended):

```bash
ExecStart=/opt/exacheck/bin/exabgp --env-file /etc/exabgp/exabgp.env server /etc/exabgp/exabgp.conf
```

[ExaCheck Configuration - Internal]: ../configuration/exacheck.md
