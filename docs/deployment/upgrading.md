---
icon: octicons/tracked-by-closed-completed-16
---

# Upgrading

Upgrading ExaCheck depends on the initial installation method.

## Upgrade Process

If ExaCheck has been installed from PyPI using `pip`, the package can be upgraded with the following command:

```bash
python3 -m pip exacheck --upgrade
```

If using the Docker image and the tag is set to `latest` (the default in the sample), simply pull and start:

```bash
docker compose pull
docker compose start
```

## Upgrade Notes

### 0.0.6

When upgrading to `0.0.5`, the `monitoring_interval` and `live_reload` options have been migrated under the [`exacheck`][ExaCheck Configuration - Internal] configuration key.

[ExaCheck Configuration - Internal]: ../configuration/exacheck.md
