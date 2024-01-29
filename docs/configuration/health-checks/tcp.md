---
icon: material/lan-connect
---

# TCP

The `tcp` health check is used to open a TCP connection to the supplied host/port. No data is sent over the connection; the test is only to validate that the port can be connected to.

## Configuration Keys

The following configuration options apply to the DNS health check method:

| Key                           | Type    | Default |
| ----------------------------- | ------- | ------- |
| [`port`](#port)               | Integer | *undef* |
| [`tcp_timeout`](#tcp-timeout) | Integer | `5`     |

### Remote Check Options

As this is a remote check, the following additional options are supported:

--8<--
snippets/checks/remote-args.md
--8<--

### Port

The `port` value defines which port the connection should be made to.

### TCP Timeout

The `tcp_timeout` controls the timeout for opening the TCP connection.

## Examples

An example TCP check:

```yaml
---

# The list of health checks
checks:

--8<--
examples/checks/tcp/basic.md
--8<--
```
