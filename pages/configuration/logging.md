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

Logging settings are stored in a key named `logging` in the configuration file. An array of logging configurations are defined in the key. If the key is not defined, file logging and syslog are disabled (the default). As this value is an array you may create as many loggers as you wish. As an example, to create a log file for route announce and withdraw events with a separate log file for health check debug logs:

```yaml
---

# Configure logging
logging:

  # Create log file for announce and withdraw events
  - log: file
    file: /var/log/exacheck/announcement.log
    events: [ announce, withdraw ]

  # Create log file for health check related information at the info level
  - log: file
    file: /var/log/exacheck/healthcheck.log
    subsystems: [ healthcheck ]
```

If configuring multiple file loggers the destination file **must** be unique per logger; you cannot have two file loggers to the same file.

## Log Filtering/Log Levels

Various options are available to filter logs to the specific events you need.

- `events`: Filter by event types such as a route being announced, an error or debugging information.
- `subsystems`: Filter by subsystems sending the log such as the master process, configuration process or an individual health check.
- `level`: Filter logs to a specific log level.
- `checks`: The list of health check names to log.

The filters may be combined together; as an example:

```yaml
---

# Configure logging
logging:

  # Create a log file to dump raw results of health checks
  - log: file
    file: /var/log/exacheck/healthcheck_raw.log
    events: [ datadump ]
    subsystems: [ healthcheck ]
```

### Log Events

The following log events are available:

| Event Name |                                         Description                                          |
| ---------- | -------------------------------------------------------------------------------------------- |
| `announce` | Route announcement events.                                                                   |
| `datadump` | Raw data dumps of objects. If using structured logging these events will be skipped.         |
| `debug`    | Debug events; verbose. The majority of messages require the log level set to debug or trace. |
| `error`    | Error events.                                                                                |
| `log`      | General log events that do not fit elsewhere.                                                |
| `withdraw` | Route withdraw events.                                                                       |

The default value is `[ announce, debug, error, log, withdraw ]`.

### Log Subsystems

The following log subsystems are available:

| Subsystem Name  |                                       Description                                       |
| --------------- | --------------------------------------------------------------------------------------- |
| `announcer`     | The route announcer.                                                                    |
| `configuration` | The configuration manager.                                                              |
| `executor`      | The check executor.                                                                     |
| `healthcheck`   | The health check itself.                                                                |
| `logging`       | The logging manager.                                                                    |
| `master`        | The master process.                                                                     |
| `utility`       | Various utilities such as the process name manager.                                     |
| `worker`        | The worker for a health check which calls the executor and manages route announcements. |

The default value is: `[ announcer, configuration, executor, healthcheck, logging, master, utility, worker ]`.

### Log Levels

The standard log levels are available: `error`, `warning`, `info`, `success`, `debug` and `trace`. The default log level is `info`.

### Checks

A list of check names to filter logging for may be set in the `checks` key. If the key has not been defined all checks will be logged.

As an example, to only log events for the check name `example` to the file `/var/log/exacheck/healthcheck_example.log`:

```yaml
---

# Configure logging
logging:

  # Create a log file to dump raw results of health checks
  - log: file
    file: /var/log/exacheck/healthcheck_example.log
    checks:
      - example
```

## Structured Logging

Structured logging can be used to allow easy parsing of logs with tools such as [lnav][lnav] however it makes it slightly harder to read the raw logs. Logs sent to syslog will default to the structured format while logs written to a file will default to a more human readable format. This configuration can be changed by setting the `structured` key to `true` or `false` depending on your needs.

## File Logging Configuration

To enable logging to a file set the `log` key to `file`. The following options are available for file logging:

|     Key      |      Type      |                                         Default                                         |                             Description                              |
| ------------ | -------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `checks`     | List\[String\] | `None`                                                                                  | The list of health check names to log.                               |
| `compress`   | Bool           | `True`                                                                                  | Compress rotated log files.                                          |
| `count`      | Integer        | `5`                                                                                     | The number of log files to keep after rotation.                      |
| `events`     | List\[String\] | `[ announce, debug, error, log, withdraw ]`                                             | The events that should be logged to the file.                        |
| `file`       | String (Path)  | `/tmp/exacheck.log`                                                                     | The file to log to. Must be writable by ExaCheck.                    |
| `formatter`  | String         | `None`                                                                                  | The [custom log format](#custom-log-format) to use.                  |
| `level`      | String         | `info`                                                                                  | The [log level](#log-levels) for the logger.                         |
| `size`       | String (Size)  | `10MB`                                                                                  | The maximum log file size before it is rotated.                      |
| `structured` | Bool           | `False`                                                                                 | Output logs in the [structured logging format](#structured-logging). |
| `subsystems` | List\[String\] | `[ announcer, configuration, executor, healthcheck, logging, master, utility, worker ]` | The subsystems that can log to the file.                             |

### File Logging Examples

To enable file logging with the default settings, create an array with only the `log` set:

```yaml
---

# Example of enabling file logging with default settings
logging:

  # The default file logger that will log to /tmp/exacheck.log
  - log: file
```

To change the logging level and use structured logging:

```yaml
---

# Example of enabling structured file logging at the debug log level
logging:

  - log: file
    level: debug
    structured: true
```

## Syslog Configuration

To enable logging to a syslog server, set `log` key to `syslog`. The following options are available for syslog:

|      Key      |               Type               |                                         Default                                         |                               Description                               |
| ------------- | -------------------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `checks`      | List\[String\]                   | `None`                                                                                  | The list of health check names to log.                                  |
| `destination` | `/dev/log`, hostname, IP address | `/dev/log`                                                                              | The location to send logs to.                                           |
| `events`      | List\[String\]                   | `[ announce, debug, error, log, withdraw ]`                                             | The events that should be logged to the syslog server.                  |
| `formatter`   | String                           | `None`                                                                                  | The [custom log format](#custom-log-format) to use.                     |
| `level`       | String                           | `INFO`                                                                                  | The [log level](#log-levels) for the logger.                            |
| `port`        | Integer                          | `514`                                                                                   | When logging to a hostname or IP address, the port to send the logs to. |
| `structured`  | Bool                             | `True`                                                                                  | Output logs in the [structured logging format](#structured-logging).    |
| `subsystems`  | List\[String\]                   | `[ announcer, configuration, executor, healthcheck, logging, master, utility, worker ]` | The subsystems that can log to the syslog server.                       |

### Syslog Examples

To enable file logging with the default settings, create an array with only the `log` set:

```yaml
---

# Example of enabling syslog with default settings
logging:

  # The default logger that will log to /dev/log (syslog local socket)
  - log: syslog
```

To send logs to the IP address `192.0.2.1` on port `514` instead of the local syslog daemon:

```yaml
---

# Example of enabling syslog with default settings
logging:

  - log: syslog
    destination: 192.0.2.1
    port: 514
```

## Custom Log Format

If you prefer to configure your own log format for messages, pass the `formatter` key to the configuration dictionary. [Loguru][Loguru] is used for logging; the [Loguru API page][Loguru API Page] provides some details on what fields are available and examples of some formats.

All logs include the following extra fields:

- `check_name`
- `event`
- `subsystem`

To reference the extra fields in your formatter use `{extra[extra_name]}` (eg. `{extra[event]}` for the event type).

As an example to log to the file `/tmp/exacheck.log` with a default logging format:

```yaml
---

# Default log format at the INFO log level for file logs
logging:
  file:
    formatter: "{time:YYYY-MM-DD HH:mm:ss.SSS} | {level: <8} | {process} | {extra[check_name]} | {file.path}:{line} | {function} | {extra[event]} | {extra[subsystem]} | {message}"
```

[lnav]: https://lnav.org/
[Loguru API Page]: https://loguru.readthedocs.io/en/stable/api/logger.html
[Loguru]: https://loguru.readthedocs.io/en/stable/overview.html
