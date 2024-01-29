---
icon: octicons/globe-24
---

# ExaCheck

The `exacheck` configuration key is used to control ExaCheck itself.

## Configuration Keys

The following configuration keys are available for ExaCheck:

| Key                                           | Type      | Default |
| --------------------------------------------- | --------- | ------- |
| [`live_reload`](#live-reload)                 | Bool      | `False` |
| [`monitoring_interval`](#monitoring-interval) | Float/Int | `30`    |

### Live Reload

Live configuration reloads may be enabled by setting `live_reload` to `True`.

#### Reload Behaviour

When enabled, during each [`monitoring_interval`](#monitoring-interval) the master process will read the configuration and look for changes. If there are changes the new configuration will be validated. Should the configuration be invalid the reload will not proceed.

If the configuration is valid any new health checks will be added and removed health checks will be terminated/withdrawn. If a health check is modified the route for that service will first be withdrawn and the health check process terminated. A new health check process will then be setup.

#### Live Reload Limitations

Only the `checks` and `notifications` configuration keys support live reloading. Any other modified keys are ignored.

### Monitoring Interval

The `monitoring_interval` option controls how often the master process checks for configuration modifications (if enabled) and that each health check process is running. If a health check process is terminated for some reason (eg. an unhandled exception) the master process will automatically respawn it at the next monitoring interval.

The default value of `30` should be fine for most use cases. Note that this value is NOT how often a health check is executed; that is controlled at the health check level.

## Examples

To enable live reload and change the monitoring interval from the default `30` seconds:

```yaml
---

# ExaCheck internal configuration
exacheck:
    # Enable live configuration reloads
    live_reload: true
    # Monitor for configuration changes and verify the health check processes are running every 60 seconds
    monitoring_interval: 60

--8<--
examples/check_footer.md
--8<--
```
