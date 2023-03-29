---
title: Health Check Config
description: Configuration available for the health checks to run.
layout: page
nav_order: 20
permalink: /configuration/health-checks.html
has_children: true
has_toc: false
parent: Configuration
---

# ExaCheck Configuration - Health Checks
{: .no_toc }

Each health check type has configuration options available depending on the specific check.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Basic Health Check Configuration Structure

Health checks are defined an array named `checks` in the configuration file. By default there are no health checks defined; it is required that you define at least one health check to run.

Each health check is **required** to have a `args` dictionary. The `args` dictionary schema depends on the type of health check that is used. As an example, a file  health check needs to know the file name to check for where as a DNS health check needs to know where to send a DNS query.

### Required Health Check Configuration

The following settings **must** be defined for each health check (they have no default value):

|    Key     |                       Type                        |                                  Description                                   |
| ---------- | ------------------------------------------------- | ------------------------------------------------------------------------------ |
| `name`     | String                                            | The name for the health check.                                                 |
| `prefixes` | Array[IP addresses/IP networks]                   | The list of IP addresses or prefixes to advertise when the service is healthy. |
| `nexthop`  | IP address, `self`                                | The next hop IP address or `self` to advertise when the service is healthy.    |
| `args`     | [Health check arguments](#health-check-arguments) | The health check to use and any configuration specific to the health check.    |

The following settings **may** be defined in the configuration for each health check. If you do not define them the default value will be used.

|    Key     |      Type      | Default |                                         Description                                         |
| ---------- | -------------- | ------- | ------------------------------------------------------------------------------------------- |
| `interval` | Integer, Float | `15`    | The interval in seconds between each health check.                                          |
| `rise`     | Integer        | `3`     | The number of consecutive health checks that are successful before the route is advertised. |
| `fall`     | Integer        | `3`     | The number of consecutive health checks that fail before the route is withdrawn.            |

### Optional Health Check Configuration

The following settings are optional.

|        Key         |          Type          | Default |                                         Description                                         |
| ------------------ | ---------------------- | ------- | ------------------------------------------------------------------------------------------- |
| `description`      | String                 | `None`  | A description for the health check. The description is not used by anything.                |
| `path_id`          | IPv4 address, Integer  | `None`  | A BGP path ID to advertise with the route. Used with BGP add-path.                          |
| `metric`           | Integer                | `None`  | A metric (MED) to advertise with the route.                                                 |
| `metric_down`      | Integer                | `None`  | If set, the metric to advertise for an unhealthy route.[^1]                                 |
| `local_preference` | Integer                | `None`  | A local preference value to advertise with the route.                                       |
| `disable`          | File path              | `None`  | A path to a file that will be used to mark the service as down.[^2]                         |
| `neighbors`        | Array[IP addresses]    | `None`  | When set, the route will only be advertised to these neighbor IPs.                          |
| `communities`      | Array[BGP communities] | `None`  | A list of BGP communities to advertise with the route.[^3]                                  |
| `as_path`          | String, Integer        | `None`  | An optional AS path to advertise with the route.                                            |

## Health Check Arguments

The `args` dictionary has the following keys that are common to all health checks:

|    Key    |      Type      | Default |                                                Description                                                |
| --------- | -------------- | ------- | --------------------------------------------------------------------------------------------------------- |
| `method`  | String         | `None`  | The actual health check method to use. This must be defined; see the below table for the list of methods. |
| `timeout` | Integer, Float | `10`    | A timeout for the entire health check to run.[^4]                                                         |

### Health Method Arguments

| Check  | Check Method Name |                                             Description                                              |
| ------ | ------------ | ---------------------------------------------------------------------------------------------------- |
| DNS    | `dns`        | Query a DNS server and optionally check/validate the response.                                       |
| File   | `file`       | Check that either a file exists or doesn't exist.                                                    |
| HTTP   | `http`       | Send a HTTP request to a web server and optionally check/validate the response.                      |
| ICMP   | `icmp`       | Ping a host to ensure that it responds.                                                              |
| NTP    | `ntp`        | Send a NTP request to a NTP server and optionally ensure that the time is within a specified offset. |
| RADIUS | `radius`     | Send a RADIUS authentication request to a RADIUS server.                                             |
| Shell  | `shell`      | Run a shell command or script and ensure a successful response code is returned.                     |
| TCP    | `tcp`        | Open a TCP connection to the specified host/port to ensure it is listening.                          |

---

[^1]: When set, the route will continue to be advertised rather than withdrawn when the service is unhealthy. This can be used to provide a fall back in case all other paths are not available.

[^2]: The disable file can be used to mark a service as down in a maintenance situation. If the file exists, the route will be withdrawn and not advertised even if the service is otherwise healthy. Health checks will be skipped while the file exists.

[^3]: Standard communities and extended communities are supported.

[^4]: The timeout value controls the over all total time of a health check to run. Some health checks may have a separate time out defined for a specific step in the check process. As an example, the DNS health check has a `dns_timeout` key which defines how long to wait for a response from the DNS server.
