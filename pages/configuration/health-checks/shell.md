---
title: Shell Health Check
description: Configuration available for the shell health check.
layout: page
nav_order: 70
permalink: /configuration/health-checks/shell.html
grand_parent: Configuration
parent: Health Check Config
---

# Health Check - Shell
{: .no_toc }

The shell health check will execute a shell command or script and check the exit code.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Shell Health Check Overview

The shell health check uses *[subprocess.run][Python subprocess.run]* to execute a shell command or script and check for a `0` exit code. If the exit code is not `0` the service is marked as unhealthy.

## Shell Health Check Arguments

The shell health check **requires** the following keys to be defined:

|    Key    |      Type      | Default |                  Description                   |
| --------- | -------------- | ------- | ---------------------------------------------- |
| `command` | String         | `None`  | The shell command or script to execute.        |
| `timeout` | Integer, Float | `10`    | The over all timeout for the check to execute. |

## Shell Health Check Configuration Samples

The following examples can be used as a template to create a file health check:

```yaml
---

# The list of health checks
checks:

  # Run the shell script /tmp/example.sh and ensure the exit code is 0
  # If the script returns success, announce the IP address 192.0.2.1 to all neighbors with a next hop of "self"
  - name: Run shell script /tmp/example.sh
    args:
      method: shell
      path: /tmp/example.sh
    prefixes:
      - 192.0.2.1

  # Run the command "/usr/local/bin/example | grep -q 'something'"
  # If the command STDOUT contained the word "something", announce the IP address 192.0.2.2 to all neighbors with a next hop of "self"
  - name: Test command /usr/local/bin/example STDOUT contains 'something'
    args:
      method: shell
      path: /usr/local/bin/example | grep -q 'something'
    prefixes:
      - 192.0.2.2
```

[Python subprocess.run]: https://docs.python.org/3/library/subprocess.html#subprocess.run
