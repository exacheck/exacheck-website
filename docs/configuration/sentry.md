---
icon: simple/sentry
---

# Sentry

The reporting to [Sentry][Sentry Homepage] using the `sentry-sdk` module can be configured with the `sentry` key.

For more information about the below configuration keys, check the [Sentry basic options documentation][Sentry Configuration - Basic Options].

## Configuration Keys

The following configuration keys are available for Sentry:

| Key                                                   | Type   | Default |
| ----------------------------------------------------- | ------ | ------- |
| [`dsn`](#dsn)                                         | String | *undef* |
| [`enabled`](#enabled)                                 | Bool   | `True`  |
| [`sample_rate`](#sample-rate)                         | Float  | `1.0`   |
| [`profiles_sample_rate`](#profiles-sample-rate)       | Float  | `0.0`   |
| [`attach_stacktrace`](#attach-stacktrace)             | Bool   | `False` |
| [`include_local_variables`](#include-local-variables) | Bool   | `True`  |
| [`debug`](#debug)                                     | Bool   | `False` |

### DSN

The DSN provided by Sentry for reporting.

### Enabled

If Sentry should be sending reports to the specified DSN. You may set this to disabled if you would like to keep the Sentry configuration but temporarily disable it.

### Sample Rate

The rate at which events are sampled for Sentry.

### Profiles Sample Rate

The rate at which samples are taken for profiling. Defaults to `0.0` (not enabled).

### Attach Stacktrace

Set `attach_stacktrace` to true to attach a stack trace to every event logged to Sentry. By default the stacktrace is only included for exceptions.

### Include Local Variables

To include a snapshot of local variables in reports, set `include_local_variables` to `True` (the default).

### Debug

To enable Sentry debug mode set `debug` to `True` (off by default). Sentry should then print helpful messages if there are issues sending events.

## Examples

```yaml
---

--8<--
examples/sentry.md
--8<--

--8<--
examples/check_footer.md
--8<--
```

[Sentry Homepage]: https://sentry.io/welcome/
[Sentry Configuration - Basic Options]: https://docs.sentry.io/platforms/python/configuration/options/
