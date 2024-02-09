---
icon: octicons/tracked-by-closed-completed-16
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

[ExaCheck Configuration - Internal]: ../configuration/exacheck.md
