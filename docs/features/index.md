---
icon: material/list-box-outline
---

# Features

ExaCheck is primarily targeted to centralized health checks where one or more servers handle health checks for multiple services.

- [Command line interface][ExaCheck Feature - CLI]
- [Live configuration reloads](#live-configuration-reloads)
- Health checks implemented in pure python where possible; no need to write scripts or use chains of commands to validate output
- [Notifications](#notifications) for announce/withdraw events and other information
- Configuration validation (if using live configuration reloads, configuration is validated before application)
- Out of the box sane defaults where possible
- JSON schema of configuration (see [configuration.json][ExaCheck Configuration Schema] for the current schema)
- [Docker deployment supported][ExaCheck Docker Deployment]
- Full IPv4 and IPv6 support
- [Choice of YAML or JSON configuration](#configuration-format)

## Live Configuration Reloads

Changes to the configuration file can optionally be applied without having to restart the ExaBGP/ExaCheck services. The live reload operation first checks to ensure the configuration is valid; if it is not valid the live reload will not proceed. Any unchanged services will not be affected.

To enable the live configuration reload feature see the [relevant configuration page][ExaCheck Configuration - Live Reload].

## Notifications

Notifications are handled using [Apprise][Apprise - GitHub]. For a list of supported notification targets see the [Apprise Wiki][Apprise - Wiki].

As with logging, notifications may be filtered per health check and for certain events. Multiple notification targets can be defined.

Check the [notification configuration][ExaCheck Configuration - Notifications] page to see examples of configuration options.

## Docker Deployment

A Docker container which includes ExaBGP, ExaCheck and all requirements is available for easy deployment. The [docker deployment][ExaCheck Docker Deployment] page includes further details.

## Configuration Format

The default configuration format is yaml. If the configuration file that is being loaded has the file extension `json` it will be loaded as a JSON document instead.

For a full list of configuration options see the [configuration page][ExaCheck Configuration] or check the [examples page][ExaCheck Examples] for inspiration.

## Process Naming

The master and worker processes are named based on the task they are performing at the time and their status. As an example:

```bash
ExaCheck Master Process [/code/configuration.yaml]: Sleeping
    ExaCheck Worker [ICMP test to Google]: Performing health check [startup]
    ExaCheck Worker [TCP test to Google port 80]: Sleeping for 14.853 seconds [rising (1/3)]
    ExaCheck Worker [File test to check if /tmp/test exists]: Sleeping for 15.000 seconds [rising (1/3)]
    ExaCheck Worker [DNS query to Cloudflare public resolver]: Sleeping for 14.952 seconds [rising (1/3)]
    ExaCheck Worker [DNS query to Cloudflare public resolver with validation]: Sleeping for 14.946 seconds [rising (1/3)]
```

[ExaCheck Feature - CLI]: cli.md
[ExaCheck Configuration]: ../configuration/index.md
[ExaCheck Examples]: ../deployment/examples.md
[ExaCheck Configuration - Live Reload]: ../configuration/live-reload.md
[ExaCheck Configuration - Notifications]: ../configuration/notifications.md
[ExaCheck Configuration Schema]: https://raw.githubusercontent.com/exacheck/exacheck/main/schema.json
[ExaCheck Docker Deployment]: ../deployment/docker.md
[Apprise - GitHub]: https://github.com/caronc/apprise
[Apprise - Wiki]: https://github.com/caronc/apprise/wiki
