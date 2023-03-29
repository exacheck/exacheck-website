---
title: DNS Health Check
description: Configuration available for the DNS health check.
layout: page
nav_order: 10
permalink: /configuration/health-checks/dns.html
grand_parent: Configuration
parent: Health Check Config
---

# Health Check - DNS
{: .no_toc }

The DNS health check is used to verify that a DNS responds and optionally verify the response contains specific content.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## DNS Health Check Overview

The DNS health check works by setting up a *[dns.resolver][Python dns.resolver]* object and sending a DNS query to the host/IP address defined in the check. By default the answer is validated to ensure there is a response and not an NXDOMAIN or other failure code. Additional validations on the response can be set if required:

- Loop through each response and check if there is a match to a provided string
- Loop through each response and check if there is a match to a provided regex

## DNS Health Check Arguments

The DNS health check **requires** the following keys to be defined:

|    Key    |         Type          | Default |                      Description                      |
| --------- | --------------------- | ------- | ----------------------------------------------------- |
| `timeout` | Integer, Float        | `10`    | The over all timeout for the check to execute.        |
| `host`    | Host name, IP address | `None`  | The host name or IP address to send the DNS query to. |
| `query`   | String                | `None`  | The name to query for.                                |

The following arguments are available for the DNS health check

|        Key        |                Type                | Default |                                          Description                                          |
| ----------------- | ---------------------------------- | ------- | --------------------------------------------------------------------------------------------- |
| `address_family`  | `ipv4`, `ipv6`                     | `None`  | Force the DNS query to a specific address family.[^1]                                         |
| `query_type`      | [DNS query type](#dns-query-types) | `soa`   | The type of query to send.                                                                    |
| `response`        | Pattern                            | `None`  | A regex to search for in the response.                                                        |
| `protocol`        | `udp`, `tcp`                       | `udp`   | The protocol to use for the DNS query.                                                        |
| `port`            | Integer                            | `53`    | The port to send the DNS request to.                                                          |
| `dns_timeout`     | Integer, Float                     | `5`     | The timeout for the DNS response from the DNS server.[^2]                                     |
| `require_resolve` | Bool                               | `True`  | Require the DNS response to return a valid answer (not a NXDOMAIN or other failure response). |

### DNS Query Types

The DNS query type may be set to one of the following values:

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

## DNS Health Check Configuration Samples

The following examples can be used as a template to create a DNS health check:

```yaml
---

# The list of health checks
checks:

  # Send a SOA query for "example.com" to 10.0.0.1 without checking the answer at all
  # If the health check is successful the IP address 192.0.2.0 will be advertised to all peers
  - name: Basic DNS query
    args:
      method: dns
      host: 10.0.0.1
      query: example.com
      require_resolve: false
    nexthop: 192.168.0.1
    prefixes:
      - 192.0.2.0

  # Send a SOA query for "example.com" to 10.0.0.2 and ensure there is a response for the query
  # If the health check is successful the IP address 192.0.2.1 will be advertised to all peers
  - name: Basic DNS query with successful response
    args:
      method: dns
      host: 10.0.0.2
      query: example.com
    nexthop: 192.168.0.2
    prefixes:
      - 192.0.2.1

  # Send an A query for "example.com" to 10.0.0.3 and ensure the response contains the IP address 10.255.0.0
  # If the health check is successful the IP address 192.0.2.2 will be advertised to all peers
  - name: DNS query with IP regex
    args:
      method: dns
      host: 10.0.0.3
      query: example.com
      response: ^10\.255\.0\.0$
    nexthop: 192.168.0.3
    prefixes:
      - 192.0.2.2

  # Send a NS query to "ns1.example.com" and and ensure the response contains an NS record matching *.example.com
  # If the health check is successful the IP address 192.0.2.3 and prefix 192.0.2.240/28 will be advertised to all peers
  - name: DNS query with string regex
    args:
      method: dns
      host: ns1.example.com
      query: example.com
      query_type: ns
      response: ^[^\.]+\.example\.com$
    nexthop: 192.168.0.4
    prefixes:
      - 192.0.2.3
      - 192.0.2.240/28
```

---

[^1]: The `host` parameter must either be an IP address of the configured address family or resolve to an IP address of the configured address family.

[^2]: The `dns_timeout` parameter must be lower than the `timeout` parameter.

[Python dns.resolver]: https://dnspython.readthedocs.io/en/latest/resolver-class.html
