---
icon: material/dns
description: The ExaCheck DNS health check is used to verify that a DNS server responds for the specified query. The response may have additional validation to ensure that it matches a requested pattern.
---

# DNS

The `dns` health check allows you to query a DNS server to ensure that it responds. Optionally, the response can be validated (eg. to ensure a certain IP address is contained within the response).

## Configuration Keys

The following configuration options apply to the DNS health check method:

| Key                                   | Type               | Default |
| ------------------------------------- | ------------------ | ------- |
| [`query`](#query)                     | String             | *undef* |
| [`query_type`](#query-type)           | String             | `soa`   |
| [`response`](#response)               | *Optional* Pattern | *undef* |
| [`tcp`](#tcp)                         | Bool               | `False` |
| [`port`](#port)                       | Integer            | `53`    |
| [`dns_timeout`](#dns-timeout)         | Integer/Float      | `5`     |
| [`require_resolve`](#require-resolve) | Bool               | `True`  |

### Remote Check Options

As this is a remote check, the following additional options are supported:

--8<--
snippets/checks/remote-args.md
--8<--

### Query

The `query` field defines the name for the DNS query. By default, a `soa` query will be sent; combined with the [`query_type`](#query-type) option you may query record types other than `soa`.

### Query Type

The `query_type` field defines the type of DNS query to send. Valid options are:

- `a`
- `aaaa`
- `any`
- `cname`
- `mx`
- `ns`
- `ptr`
- `soa`
- `srv`
- `txt`

The `soa` query type is used by default.

### Response

The `response` field can define a regex/pattern of valid responses. As an example, you may want to verify that a certain IP address is returned in the response.

### TCP

By default DNS queries are sent using UDP; to use TCP instead set the `tcp` option to `True`.

### Port

The `port` option can be used to send DNS queries to an alternative port other than `53`.

### DNS Timeout

A 5 second timeout is applied to DNS queries; you may raise or lower the `timeout` value if required.

### Require Resolve

The `require_resolve` option can be disabled to allow any type of DNS response including NXDOMAIN. If set to the default value of `True`, responses from the DNS server must return a valid result.

## Examples

Some examples of DNS health checks:

=== "Basic"

    A basic configuration:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/dns/basic.md
    --8<--
    ```

=== "CNAME"

    To validate a CNAME record contains expected content:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/dns/cname-check.md
    --8<--
    ```

=== "IP Regex"

    To send a `A` query to a name server and validate the returned IP address with a regex:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/dns/ip-regex.md
    --8<--
    ```
