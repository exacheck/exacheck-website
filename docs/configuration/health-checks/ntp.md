---
icon: material/timer
---

# NTP

The `ntp` health check will send a NTP query and optionally validate that the server offset and stratum value is within the supplied parameters.

## Configuration Keys

The following configuration options apply to the NTP health check method:

| Key                           | Type                     | Default |
| ----------------------------- | ------------------------ | ------- |
| [`port`](#port)               | Integer                  | `123`   |
| [`version`](#version)         | Integer                  | `2`     |
| [`ntp_timeout`](#ntp-timeout) | Integer/Float            | `5`     |
| [`max_offset`](#max-offset)   | *Optional* Integer/Float | *undef* |
| [`max_stratum`](#max-stratum) | *Optional* Integer       | *undef* |


### Remote Check Options

As this is a remote check, the following additional options are supported:

--8<--
snippets/checks/remote-args.md
--8<--

### Port

By default, the `port` value is set to the well known port value `123`. If the NTP server is listening on a different port change this port to match.

### Version

Version 2 NTP queries are sent by default for the health check. Support `version` values are:

- `2`
- `3`

### NTP Timeout

The `ntp_timeout` option determines how long the NTP request is allowed to wait for a response.

### Max Offset

The `max_offset` value can be used to ensure the time contained within the NTP response is within a certain offset.

### Max Stratum

The `max_stratum` value can be used to ensure the NTP server is within a certain stratum value. Valid options are integers between `1` to `15`.

## Examples

These are some configuration examples for the NTP health check:

=== "Basic Query"

    To send a NTP query and validate there is a response:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/ntp/basic.md
    --8<--
    ```

=== "NTP Stratum"

    To ensure the NTP server is at least stratum 2:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/ntp/stratum.md
    --8<--
    ```
