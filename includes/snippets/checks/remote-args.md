| Key                                 | Type              | Default |
| ----------------------------------- | ----------------- | ------- |
| [`host`](#host)                     | String            | *undef* |
| [`address_family`](#address-family) | *Optional* String | *undef* |
| [`all_valid`](#all-valid)           | Bool              | `False` |

##### Host

The `host` field contains the IP address or hostname that the health check should be executed against. If a hostname is supplied, each health check execution will perform a DNS resolution to ensure the current IP is used.

As the hostname may resolve to multiple addresses and/or address families (eg. IPv4 and IPv6) the [`address_family`](#address-family) and [`all_valid`](#all-valid) options can be used to control what happens in those situations.

--8<--
snippets/checks/remote-host-warning.md
--8<--

##### Address Family

The `address_family` key is used when `host` is set to a hostname. Should the hostname resolve to an IPv4 and IPv6 address you may want the check to only be sent to a single address family rather than both.

The values `ipv4` or `ipv6` are supported. If not defined there is no filtering for IPv4 or IPv6 addresses applied.

##### All Valid

The `all_valid` key is used when `host` is set to a hostname. If the hostname resolves to multiple IP addresses and `all_valid` is set to `True`, the health check will be executed against all IP addresses available. Should the health check to any IP address fail the service will be marked as down.

If set to the default `False` value a successful health check from any IP address is considered valid and the service will be marked up.