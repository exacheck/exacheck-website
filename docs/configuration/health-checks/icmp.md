---
icon: material/format-text-wrapping-overflow
---

# ICMP

The `icmp` health check is used to validate that a host responds to ICMP ping requests. The number of ping requests, the interval between the requests and maximum jitter/latency/loss values may be defined.

## Configuration Keys

The following configuration options apply to the ICMP health check method:

| Key                             | Type                     | Default |
| ------------------------------- | ------------------------ | ------- |
| [`count`](#count)               | Integer                  | `3`     |
| [`interval`](#interval)         | Integer/Float            | `0.25`  |
| [`icmp_timeout`](#icmp-timeout) | Integer/Float            | `2`     |
| [`privileged`](#privileged)     | Bool                     | `False` |
| [`max_loss`](#max-loss)         | Integer                  | `0`     |
| [`max_latency`](#max-latency)   | *Optional* Integer/Float | *undef* |
| [`max_jitter`](#max-jitter)     | *Optional* Integer/Float | *undef* |

### Remote Check Options

As this is a remote check, the following additional options are supported:

--8<--
snippets/checks/remote-args.md
--8<--

### Count

By default, 3 ping requests will be sent. The `count` value may be changed should you want more/less requests.

### Interval

The `interval` value sets the delay being subsequent ping requests.

### ICMP Timeout

To limit the potential response time for individual ICMP requests the `icmp_timeout` is used. The timeout value must be lower than the health checks `timeout` value * `count`.

### Privileged

If set to `False` (the default), the Python module is used to generate the ICMP packets. If set to `True` the kernel will be used instead. For more information see the [icmplib root privileges page][icmplib - Without Root Privileges] on GitHub.

### Max Loss

The `max_loss` option can be adjusted to allow for packet loss. The default value of `0` means no responses may be lost.

### Max Latency

If the `max_latency` option is set, ping responses must be received within the supplied amount of milliseconds.

### Max Jitter

If the `max_jitter` option is set, the jitter between the ping responses must be within the supplied number of milliseconds.

## Examples

Some examples of ICMP health checks:

=== "Basic"

    A basic configuration:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/icmp/basic.md
    --8<--
    ```

=== "Latency"

    To validate that latency is within 20ms across 5 pings:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/icmp/latency.md
    --8<--
    ```

=== "Packet Loss Allowed"

    To validate that latency is within 250ms and allow up to 50% packet loss:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/icmp/packetloss.md
    --8<--
    ```

[icmplib - Without Root Privileges]: https://github.com/ValentinBELYN/icmplib/blob/main/docs/6-use-icmplib-without-privileges.md