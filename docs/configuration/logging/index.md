---
icon: octicons/log-16
---

# Logging

By default, logs are only sent to STDOUT. Optionally logs may be sent to one or more log files or syslog servers.

Logs to each defined target can be filtered - you may want to log certain health check events to a log file and other events to a remote syslog server. You may also define different log levels per log target.

## Configuration Keys

Logging is configured as an array of `LogMethods` objects. The following top level configuration keys are available for each object and apply to both file and syslog targets:

| Key                         | Type                    | Default                                                                                                               |
| --------------------------- | ----------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [`method`](#method)         | String                  | `info`                                                                                                                |
| [`level`](#level)           | String                  | `info`                                                                                                                |
| [`formatter`](#formatter)   | *Optional* String       | *undef*                                                                                                               |
| [`events`](#events)         | String                  | `["announce", "error", "info", "withdraw"]`                                                                           |
| [`subsystems`](#subsystems) | List[String]            | `["announcer", "configuration", "executor", "healthcheck", "logging", "master", "notification", "utility", "worker"]` |
| [`checks`](#checks)         | *Optional* List[String] | *undef*                                                                                                               |

### Method

These log methods are supported:

- `file`: Log to a file.
- `syslog`: Log to a remote syslog server with UDP or TCP.

!!! warning

    You MUST add the method specific configuration noted below otherwise the configuration will be invalid.

#### Method Specific Configuration

The file and syslog methods require specific configuration. Check the relevant page depending on the log method:

- [File Logging][ExaCheck Configuration - File Logging]
- [Syslog Logging][ExaCheck Configuration - Syslog Logging]

### Level

The level of messages to send to the logging target. Available options are:

- `error`
- `warning`
- `info`
- `success`
- `debug`
- `trace`

### Formatter

A custom log format string can be provided if you need to change the formatting. As an example, the default log format for STDERR logs is:

```python
<green>{time:YYYY-MM-DD HH:mm:ss.SSS}</green> | <level>{level: <8}</level> | <light-blue>PID {process: <8}</light-blue> | <magenta>{file.path}:{line} {function}()</magenta> | <cyan>{extra[check_name]}</cyan> | <green>{extra[subsystem]}/{extra[event]}</green> | <level>{message}</level>
```

### Events

The list of events that may be logged for this target. The following events are supported:

- `announce`: Route announcements
- `withdraw`: Route withdrawals
- `error`: Error logs
- `info`: General information
- `debug`: Verbose debugging information
- `datadump`: Dumps of various data for debugging

### Subsystems

Filtering may be applied by subsystem (the part of ExaCheck that is generating the log). The list of subsystems available are:

- `announcer`: The route announcement/withdrawal manager
- `configuration`: Configuration manager
- `executor`: The check executor
- `healthcheck`: Messages from health checks themselves
- `logging`: Messages from the logging manager
- `master`: Messages from the master process
- `notification`: Messages generated from notifications
- `utility`: Various utilities that do not fit elsewhere
- `worker`: Worker related messages

### Checks

A list of health checks may be provided; events will only be sent to the logging target if they are generated by the defined health checks.

## Examples

To configure both syslog and file based logging:

```yaml
---

logging:

--8<--
examples/logging/file/basic.md
--8<--

--8<--
examples/logging/syslog/tcp.md
--8<--

--8<--
examples/check_footer.md
--8<--
```

For more complete examples, check the relevant method page.

[ExaCheck Configuration - File Logging]: file.md
[ExaCheck Configuration - Syslog Logging]: syslog.md
