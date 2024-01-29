---
icon: simple/sentry
---

# Sentry

The reporting to [Sentry][Sentry Homepage] using the `sentry-sdk` module can be configured with the `sentry` key.

## Configuration Keys

The following configuration keys are available for Sentry:

| Key                                             | Type   | Default |
| ----------------------------------------------- | ------ | ------- |
| [`dsn`](#dsn)                                   | String | *undef* |
| [`enabled`](#enabled)                           | Bool   | `True`  |
| [`sample_rate`](#sample-rate)                   | Float  | `1.0`   |
| [`profiles_sample_rate`](#profiles-sample-rate) | Float  | `0.0`   |

### DSN

The DSN provided by Sentry for reporting.

### Enabled

If Sentry should be sending reports to the specified DSN. You may set this to disabled if you would like to keep the Sentry configuration but temporarily disable it.

### Sample Rate

The rate at which events are sampled for Sentry.

### Profiles Sample Rate

The rate at which samples are taken for profiling. Defaults to `0.0` (not enabled).

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
