---
icon: material/heart-pulse
---

# Health Checks

Health checks are the heart of ExaCheck; a list of health checks can be defined in the `checks` key.

There are two categories of health checks:

- Local: Local checks are for scripts executed on the local machine or testing if a file exists/doesn't exist.
- Remote: Remote checks are anything that uses the network. This may be a HTTP request, DNS request etc. The remote checks have additional options not available to local checks.

## Configuration Keys

The following top level configuration keys apply to health checks.

| Key                                     | Type                            | Default |
| --------------------------------------- | ------------------------------- | ------- |
| [`name`](#name)                         | String                          | *undef* |
| [`args`](#args)                         | Dict                            | *undef* |
| [`prefixes`](#prefixes)                 | List[IPNetwork]                 | *undef* |
| [`nexthop`](#nexthop)                   | String                          | `self`  |
| [`interval`](#interval)                 | Integer/Float                   | `15`    |
| [`rise`](#rise)                         | Integer                         | `3`     |
| [`fall`](#fall)                         | Integer                         | `3`     |
| [`description`](#description)           | *Optional* String               | *undef* |
| [`path_id`](#path-id)                   | *Optional* Integer/IPv4 Address | *undef* |
| [`metric`](#metric)                     | *Optional* Integer              | *undef* |
| [`metric_down`](#metric-down)           | *Optional* Integer              | *undef* |
| [`local_preference`](#local-preference) | *Optional* Integer              | *undef* |
| [`disable`](#disable)                   | *Optional* String               | *undef* |
| [`neighbors`](#neighbors)               | *Optional* List[IPAddress]      | *undef* |
| [`communities`](#communities)           | *Optional* List[String]         | *undef* |
| [`as_path`](#as-path)                   | *Optional* String               | *undef* |

### Name

The name of this health check. The name is used for logging purposes as well as optional filtering of logs/notifications.

### Args

The `args` key contains the actual arguments for each health check. These are things such as the health check type and parameters for the service to be marked as up.

!!! warning

    The `args` key **must** contain a `method` value. The method is used to configure which health check needs to run. The current list of available health check methods are:

    | Method Name                                      | Description                                                                     |
    | ------------------------------------------------ | ------------------------------------------------------------------------------- |
    | [`dns`][ExaCheck Configuration - DNS Method]     | Query a DNS server and optionally validate the response.                        |
    | [`file`][ExaCheck Configuration - File Method]   | Test if a file path exists or doesn't exist.                                    |
    | [`http`][ExaCheck Configuration - HTTP Method]   | Send HTTP or HTTPS requests and validate the response and/or SSL certificates.  |
    | [`icmp`][ExaCheck Configuration - ICMP Method]   | Send ICMP ping requests and validate the latency is within an acceptable range. |
    | [`ntp`][ExaCheck Configuration - NTP Method]     | NTP health check for time servers.                                              |
    | [`shell`][ExaCheck Configuration - Shell Method] | Run the supplied script and validate the exit code returned is successful.      |
    | [`tcp`][ExaCheck Configuration - TCP Method]     | Validate a TCP connection can be opened to the supplied host/port.              |

Both local and remote health checks support the `timeout` key which defines the time limit for how long a check execution can take. This timeout prevents a health check being in a stuck condition; the check will be terminated if the timeout is reached. By default the timeout is set to 10 seconds.

#### Remote Check Args

Remote health check methods (such as `http`, `icmp`, `dns`) support the following common args:

--8<--
snippets/checks/remote-args.md
--8<--

### Prefixes

The `prefixes` array contains the list of IP addresses or networks to advertise when the check is considered up. IPv4 or IPv6 addresses/networks may be defined. The addresses/networks must all be of the same address family; you cannot mix IPv4 and IPv6 in the same health check (instead you would define an IPv4 and IPv6 health check).

!!! warning

    If the [`nexthop`](#nexthop) value is set to an IP address, the addresses/networks must be of the same address family.

### Nexthop

The `nexthop` attribute defines the next hop to advertise for the addresses/prefixes for the service. May be set to an IPv4 or IPv6 address or the value `self`.

### Interval

The `interval` value defines how often the health check is executed in seconds.

### Rise

The `rise` value defines how many health checks must be successful in a row before the service is considered as up.

### Fall

The `fall` value defines how many health checks must fail in a row before the service is considered as down.

### Description

The `description` is an optional value which is not used by ExaCheck; you may enter a description to make the configuration easier to read.

### Path ID

The `path_id` attribute can be used for handling of ECMP routes. If there is a single server running ExaCheck and there are two different health checks which advertise the same prefix, the path ID must be set to identify the route. If it is not defined it will result in unpredictable behaviour for announcements/withdrawals and ECMP may fail to work depending on the router vendor.

### Metric

If the `metric` value is set, routes will be advertised with this MED value.

#### Metric Down

If the `metric_down` value is set, rather than withdrawing routes with failed health checks the route will be announced with the supplied metric.

!!! danger

    This feature is currently not working.

### Local Preference

The `local_preference` value may be defined to advertise routes with a specific local preference.

### Disable

The `disable` key may be set to a path on the local host filesystem. If the file path exists it will result in the service being marked as down and the routes withdrawn.

This can be used to take down a service manually by touching a file (eg. for maintenance).

### Neighbors

By default, ExaBGP will advertise the supplied route to all available neighbors. If you have multiple neighbors configured and you want to filter an advertisement to one or more specific neighbors only, set the `neighbors` attribute to a list of IP addresses.

### Communities

To add BGP communities to advertised routes set the `communities` attribute to a list of BGP community values.

Regular, large and extended BGP communities are supported.

### AS Path

To override the AS path of advertised routes you may set the `as_path value`.

## Examples

These are some configuration examples of some health checks.

```yaml
---

# Various example health checks
checks:

--8<--
examples/checks/dns/basic.md
--8<--

--8<--
examples/checks/icmp/basic.md
--8<--

--8<--
examples/checks/file/basic.md
--8<--

--8<--
examples/checks/shell/basic.md
--8<--
```

[ExaCheck Configuration - DNS Method]: dns.md
[ExaCheck Configuration - File Method]: file.md
[ExaCheck Configuration - HTTP Method]: http.md
[ExaCheck Configuration - ICMP Method]: icmp.md
[ExaCheck Configuration - NTP Method]: ntp.md
[ExaCheck Configuration - Shell Method]: shell.md
[ExaCheck Configuration - TCP Method]: tcp.md
