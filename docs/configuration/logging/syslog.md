---
icon: material/cloud-print
---

# Syslog

The `syslog` log method can be used to send logs to a local socket or remote syslog servers using UDP or TCP.

## Configuration Keys

The following configuration keys apply to only the syslog target. The [logging page][ExaCheck Configuration - Logging] lists general configuration which is shared with the `file` logger.

| Key                           | Type    | Default    |
| ----------------------------- | ------- | ---------- |
| [`structured`](#structured)   | Bool    | `True`     |
| [`destination`](#destination) | String  | `/dev/log` |
| [`port`](#port)               | Integer | `514`      |
| [`protocol`](#protocol)       | String  | `udp`      |

### Structured

--8<--
snippets/logging/structured.md
--8<--

### Destination

The destination to send logs to. May be a path to a socket, an IP address or hostname.

### Port

If sending logs to a remote host, the port to send them to.

### Protocol

The protocol to send the syslog messages with when logging to a remote host. Valid options are `tcp` or `udp`.

!!! info

    UDP logging is preferred to ensure there are no delays should the syslog destination not be reachable.

## Examples

These are some examples of what can be configured for the `syslog` target.

### Local Socket

Some examples of configuring logging to sockets:

=== "Minimal"

    A minimal configuration for a single log target:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/syslog/socket.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

=== "Multiple Targets"

    A configuration for logging to multiple sockets with filtering:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/syslog/socket.md
    --8<--

    --8<--
    examples/logging/syslog/socket-filtering.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

### Remote Syslog Servers

These examples are for logging to remote syslog servers.

=== "UDP (Minimal)"

    A minimal UDP configuration looks like this:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/syslog/basic.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

=== "UDP"

    The port may be changed and structured logs disabled:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/syslog/udp.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

=== "TCP"

    TCP logging is configured the same way; the protocol just needs to be changed:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/syslog/tcp.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

=== "Multiple Targets"

    Multiple targets may be defined as usual:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/syslog/udp.md
    --8<--

    --8<--
    examples/logging/syslog/tcp.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

[ExaCheck Configuration - Logging]: index.md
