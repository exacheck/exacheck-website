---
icon: material/reload
---

# Live Reload

The live configuration reload option allows you to control the behaviour for changes to the configuration file. By default, the feature is disabled - any changes you make to the configuration file require the ExaCheck process to be restarted.

## Reload Behaviour

When enabled, during each [`monitoring_interval`][ExaCheck Configuration - Monitoring Interval] the master process will read the configuration and look for changes. If there are changes the new configuration will be validated. Should the configuration be invalid the reload will not proceed.

If the configuration is valid any new health checks will be added and removed health checks will be terminated/withdrawn. If a health check is modified the route for that service will first be withdrawn and the health check process terminated. A new health check process will then be setup.

## Examples

To enable live configuration reloading:

```yaml
---

# Enable live reloads
live_reload: true

--8<--
examples/check_footer.md
--8<--
```

## Limitations

Only the `checks` and `notifications` configuration keys support live reloading. Any other modified keys are ignored.

[ExaCheck Configuration - Monitoring Interval]: index.md#monitoring-interval
