---
title: File Health Check
description: Configuration available for the file health check.
layout: page
nav_order: 20
permalink: /configuration/health-checks/file.html
grand_parent: Configuration
parent: Health Check Config
---

# Health Check - File
{: .no_toc }

The file health check is used to validate that either a file is present or not present.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## File Health Check Overview

The file check uses *[os.access][Python os.access]* to check for file existence. By default the file must exist for the service to be marked as healthy. The check may be configured to ensure that a file **doesn't** exist by setting the `exists` key to `false`.

## File Health Check Arguments

The file health check **requires** the following keys to be defined:

|    Key    |      Type      | Default |                  Description                   |
| --------- | -------------- | ------- | ---------------------------------------------- |
| `exists`  | Bool           | `True`  | Ensure that the file exists.                   |
| `path`    | Path           | `None`  | The path to the file to test.                  |
| `timeout` | Integer, Float | `10`    | The over all timeout for the check to execute. |

## File Health Check Configuration Samples

The following examples can be used as a template to create a file health check:

```yaml
---

# The list of health checks
checks:

  # Ensure the file /tmp/test1 exists
  # If the file exists, announce the IP address 192.0.2.1 to all neighbors with a next hop of "self"
  - name: File test for /tmp/test1 existence
    args:
      method: file
      path: /tmp/test1
    prefixes:
      - 192.0.2.1

  # Ensure the file /tmp/test2 absence
  # If the file does not exist, announce the IP address 192.0.2.2 to all neighbors with a next hop of "self"
  - name: File test for /tmp/test2 absence
    args:
      method: file
      path: /tmp/test2
      exists: false
    prefixes:
      - 192.0.2.2
```

[Python os.access]: https://docs.python.org/3/library/os.html#os.access
