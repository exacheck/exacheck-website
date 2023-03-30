---
title: ExaCheck Config
description: General configuration options for ExaCheck.
layout: page
nav_order: 10
permalink: /configuration/exacheck.html
parent: Configuration
---

# ExaCheck Configuration - ExaCheck Settings
{: .no_toc }

There are various ExaCheck specific settings to control the behaviour of ExaCheck. All settings have a default value; you should only need to alter them if you have a specific reason to.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## ExaCheck Settings

The ExaCheck settings are defined at the top level of the YAML dictionary. The following keys are available:

|          Key          |      Type      | Default |                                                            Description                                                             |
| --------------------- | -------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `live_reload`         | Bool           | `False` | Enable [live configuration reloads](#live-configuration-reload).                                                                   |
| `monitoring_interval` | Integer, Float | `30`    | The interval in settings for [monitoring processes/configuration changes](#monitoring-interval) to ensure they are healthy. |

## Live Configuration Reload

The `live_reload` configuration key can be used to control if the live reload setting is enabled. When enabled, the configuration file is checked every *`monitoring_interval`* seconds for changes. If the content of the file differs the configuration file will then be parsed/validated.

If the configuration file is valid the configuration values for each check will be compared to find any additions/removals/modifications. Should any checks have changes the following happens:

1. The route(s) are first withdrawn for the health check.
2. The process for the health check is terminated.
3. A new process for the health check is spawned.
4. The checks proceed as usual.

{: .warning }
The option is set to `False` by default as this behaviour may be undesirable in certain situations. Use caution if enabling this option!

If live reloading is disabled you cannot enable it without restarting ExaCheck. Likewise, if live reloading is enabled and you disable it the only way to enable it again is by restarting ExaCheck.

## Monitoring Interval

The monitoring interval configures how often the ExaCheck master process checks the health check processes and tests for any configuration changes. If a health check process fails due to an unhandled exception it will be re-spawned automatically in this monitoring loop.

## Configuration Examples

The following configuration shows the default values:

```yaml
---

# Live reloads disabled by default
live_reload: false

# Health check processes are monitored every 30 seconds
monitoring_interval: 30
```
