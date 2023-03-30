---
title: Logging Config
description: Configuration for logging of health checks to files or a remote syslog server.
layout: page
nav_order: 30
permalink: /configuration/logging.html
parent: Configuration
---

# ExaCheck Configuration - Logging
{: .no_toc }

By default, logs are only output to STDERR. To configure [file based logging](#file-logging-configuration) or [syslog](#syslog-configuration) (local or remote) follow the steps below.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Basic Logging Configuration Structure

Logging settings are stored in a dictionary named `logging` in the configuration file. If the dictionary is not defined, file logging and syslog are disabled (the default).

If the dictionary is defined, one (or both) of the following keys must exist:

- `file`: File based logging configuration
- `syslog`: Syslog based logging configuration

To enable file and/or syslog logging with the default settings simply create an empty dictionary.

## Log Levels

The following log levels are available (in order of least verbose to most verbose):

- `ERROR`
- `WARNING`
- `INFO`
- `SUCCESS`
- `DEBUG`
- `TRACE`

## Structured Logging

Structured logging can be used to allow easy parsing of logs with tools such as [lnav][lnav] however it makes it slightly harder to read the raw logs. Logs sent to syslog will default to the structured format while logs written to a file will default to a more human readable format. This configuration can be changed by setting the `structured` key to `True` or `False` depending on your needs.

## File Logging Configuration

The `file` logging dictionary has the following configuration keys available:

|     Key      |     Type      |       Default       |                             Description                              |
| ------------ | ------------- | ------------------- | -------------------------------------------------------------------- |
| `level`      | String        | `INFO`              | The [log level](#log-levels) for the logger.                         |
| `structured` | Bool          | `False`             | Output logs in the [structured logging format](#structured-logging). |
| `file`       | String (Path) | `/tmp/exacheck.log` | The file to log to. Must be writable by ExaCheck.                    |
| `size`       | String (Size) | `10MB`              | The maximum log file size before it is rotated.                      |
| `count`      | Integer       | `5`                 | The number of log files to keep after rotation.                      |
| `compress`   | Bool          | `True`              | Compress rotated log files.                                          |
| `formatter`  | String        | `None`              | The [custom log format](#custom-log-format) to use.                  |

### File Logging Examples

To enable file logging with the default settings, create an empty dictionary:

```yaml
---

# Example of enabling file logging with default settings
logging:
  file: {}
```

To change the logging level and use structured logging:

```yaml
---

# Example of enabling structured file logging at the DEBUG log level
logging:
  file:
    level: DEBUG
    structured: true
```

## Syslog Configuration

Syslog can be used to send logs to a local syslog daemon or a remote syslog host. By default, syslogs will be written to the local socket `/dev/log`.

The `syslog` dictionary has the following keys available:

|      Key      |               Type               |  Default   |                               Description                               |
| ------------- | -------------------------------- | ---------- | ----------------------------------------------------------------------- |
| `destination` | `/dev/log`, hostname, IP address | `/dev/log` | The location to send logs to.                                           |
| `formatter`   | String                           | `None`     | The [custom log format](#custom-log-format) to use.                     |
| `level`       | String                           | `INFO`     | The [log level](#log-levels) for the logger.                            |
| `port`        | Integer                          | `514`      | When logging to a hostname or IP address, the port to send the logs to. |
| `structured`  | Bool                             | `True`     | Output logs in the [structured logging format](#structured-logging).    |

### Syslog Examples

To enable syslog with the default settings, create an empty dictionary:

```yaml
---

# Example of enabling syslog with default settings
logging:
  syslog: {}
```

To send logs to the IP address `192.0.2.1` on port `514` instead of the local syslog daemon:

```yaml
---

# Example of enabling syslog with default settings
logging:
  syslog:
    destination: 192.0.2.1
    port: 514
```

## Custom Log Format

If you prefer to configure your own log format for messages, pass the `formatter` key to the `file` or `syslog` configuration dict. [Loguru][Loguru] is used for logging; the [Loguru API page][Loguru API Page] provides some details on what fields are available and examples of some formats.

To aid in debugging, the `extra[process_name]` variable is always defined which contains the name of the process sending the log. The process name is set to the name of the health check or master for the monitoring process.

As an example, a file based logger with the default format looks like this:

```yaml
---

# Default log format at the INFO log level for file logs
logging:
  file:
    formatter: "{time:YYYY-MM-DD HH:mm:ss.SSS} | {level: <8} | [{process}] {extra[process_name]} | {file}:{line} | {message}"
```

[lnav]: https://lnav.org/
[Loguru API Page]: https://loguru.readthedocs.io/en/stable/api/logger.html
[Loguru]: https://loguru.readthedocs.io/en/stable/overview.html
