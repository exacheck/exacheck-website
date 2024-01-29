---
icon: octicons/tracked-by-closed-completed-16
---

# Upgrading

As this is currently in alpha, there are no upgrade notes available yet. If there are any breaking changes in future they will be listed here.

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
