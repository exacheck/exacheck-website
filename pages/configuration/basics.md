---
title: Configuration Basics
description: ExaCheck configuration file basic overview.
layout: page
nav_order: 0
permalink: /configuration/basics
parent: Configuration
---

# ExaCheck Configuration Basics
{: .no_toc }

ExaCheck reads from a YAML configuration file containing the list of checks. By default, the configuration file will be loaded from `/etc/exabgp/exacheck.yaml`.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Base Structure

The basic configuration schema looks like this:

```yaml
---

# Enable auto reload of configuration
live_reload: true

# Use processes for handling health checks
executor: processes

# The list of health checks
checks:
  - name: Send DNS query to 192.0.2.1
    description: Example DNS based health check to 192.0.2.1; advertise 192.0.2.55 if healthy
    args:
      method: dns
      host: 192.0.2.1
      query: mydomain.com
    prefixes:
      - 192.0.2.255
    nexthop: 192.0.2.1
```

## Check Configuration

The heart of ExaCheck is the actual health checks. The health checks are configured in the `checks` key (see above example). The following health checks are available:

| Check  | Check Method |                                             Description                                              |
| ------ | ------------ | ---------------------------------------------------------------------------------------------------- |
| DNS    | `dns`        | Query a DNS server and optionally check/validate the response.                                       |
| File   | `file`       | Check that either a file exists or doesn't exist.                                                    |
| HTTP   | `http`       | Send a HTTP request to a web server and optionally check/validate the response.                      |
| ICMP   | `icmp`       | Ping a host to ensure that it responds.                                                              |
| NTP    | `ntp`        | Send a NTP request to a NTP server and optionally ensure that the time is within a specified offset. |
| RADIUS | `radius`     | Send a RADIUS authentication request to a RADIUS server.                                             |
| Shell  | `shell`      | Run a shell command or script and ensure a successful response code is returned.                     |
| TCP    | `tcp`        | Open a TCP connection to the specified host/port to ensure it is listening.                          |

### Check Arguments

There is specific configuration unique to each check method (eg. for the `shell` check it needs to know what command to run where as the `tcp` check needs to know a hostname/port to connect to). All check method configuration is defined in the `args` parameter.

## Configuration Schema

The full JSON schema for the configuration is available in the repository ([configuration.json][ExaCheck Configuration Schema]); it may also be generated directly with the ExaCheck command line interface:

```bash
exacheck schema > configuration.json
```

The configuration schema can be used to visualize the available configuration options using a tool such as [JSON Crack] or be used with an IDE when editing the configuration file.

### VS Code Editing

If using VS Code with the [YAML Language Server] the following header may be set in the configuration file:

```yaml
---
# yaml-language-server: $schema=/code/configuration.json
```

VS Code will then be able to perform basic configuration validation and provide hints to aid you.

[ExaCheck Configuration Schema]: https://github.com/exacheck/exacheck/blob/main/configuration.json
[JSON Crack]: https://jsoncrack.com/editor
[YAML Language Server]: https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml