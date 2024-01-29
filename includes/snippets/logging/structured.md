Structured logging can be enabled/disabled with the `structured` option. By default, logs sent to syslog servers are structured while file logs are not structured. An example of structured logs:

```bash
--8<--
snippets/logging/structured-example.md
--8<--
```

If disabled, the logs will look like this:

```bash
--8<--
snippets/logging/standard-example.md
--8<--
```
