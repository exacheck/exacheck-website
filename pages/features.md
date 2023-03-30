---
title: Features
description: ExaCheck features and tips and configuration hints.
layout: page
nav_order: 10
permalink: /features.html
---

# ExaCheck Features
{: .no_toc }

ExaCheck is primarily targeted to centralized health checks; see the main features below.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Feature Overview

- [Command line interface][ExaCheck Command Line Interface] to test the configuration and run ExaCheck easily
- [Live configuration reloads][ExaCheck Configuration - Live Reload] (adding/modifying/removing services)
- Health checks implemented in pure python where possible; no need to write scripts or use chains of commands to validate output
- [Detailed logging](#logging) available
- Configuration validation (if using live configuration reloads, configuration is validated before application)
- Out of the box sane defaults where possible
- JSON schema of configuration (see [configuration.json][ExaCheck Configuration Schema] for the current schema)
- [Easy Docker deployment][ExaCheck Docker Deployment]
- Full IPv4 and IPv6 support; configurable per health check

## Configuration

These are configuration specific features. For a basic overview of the configuration see the [configuration basics][ExaCheck Configuration Basics] page.

### Configuration Reloads

The configuration can have [optional live reloads][ExaCheck Configuration - Live Reload] enabled. Simply changing the configuration file will cause ExaCheck to validate and apply changes automatically without needing to restart any services.

### Configuration Validation

[Pydantic][Pydantic] is used for configuration validation and to ensure correct data types are provided. If the configuration is not valid, ExaCheck will not start. If ExaCheck is already running and live reloads are enabled the invalid configuration will be skipped without change.

## Logging

[Loguru][Loguru] is used for logging. By default, logs are output to STDOUT only. Extensive debugging/trace logging is available to help troubleshoot potential problems; log levels can be configured per-log destination.

Optionally, ExaCheck can be configured to log to a file or to syslog (remote syslog servers supported). If using file based logging, the rotation/compression of the log files is managed by ExaCheck for you.

For configuration examples and further information see the [logging configuration page][ExaCheck Configuration - Logging].

### Structured Logging

Logs output to a syslog server default to a structured logging format to allow easy parsing of logs. Logs output to a file can optionally have the structured logging format enabled; this is useful if using a tool such as [lnav][lnav].

## Process Naming

ExaCheck processes are named based on the current task they are performing. As an example, the process list will show tasks like this:

```bash
ExaCheck Master Process [/code/configuration.yaml]: Sleeping for 30 seconds
  ExaCheck Worker [ICMP test to Google]: Sleeping for 13.908 seconds [up]
  ExaCheck Worker [TCP test to Google port 80]: Sleeping for 14.952 seconds [up]
  ExaCheck Worker [File test to check if /tmp/test exists]: Sleeping for 14.999 seconds [up]
  ExaCheck Worker [DNS query to Cloudflare public resolver]: Sleeping for 14.954 seconds [up]
  ExaCheck Worker [DNS query to Cloudflare public resolver with validation]: Sleeping for 14.957 seconds [up]
```

## Process Monitoring

The health check processes that are spawned are monitored on a monitoring loop. Each health check process should handle its own exceptions however in the event of an unhandled exception the master process will re-spawn it automatically.

[ExaCheck Command Line Interface]: /cli.html
[ExaCheck Configuration - Live Reload]: /configuration/exacheck.html#live-configuration-reload
[ExaCheck Configuration - Logging]: /configuration/logging.html
[ExaCheck Configuration Basics]: /configuration/basics.html
[ExaCheck Configuration Schema]: https://github.com/exacheck/exacheck/blob/main/configuration.json
[ExaCheck Docker Deployment]: /deployment/docker.html
[lnav]: https://lnav.org/
[Loguru]: https://github.com/Delgan/loguru
[Pydantic]: https://docs.pydantic.dev/
