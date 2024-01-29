---
icon: material/head-question
---

# Examples

These are some example configurations for ExaBGP + ExaCheck. The health check configuration examples are taken from the relevant health check configuration page.

## ExaBGP Configuration

[ExaBGP][ExaBGP GitHub] needs to be configured to execute ExaCheck. By default the ExaBGP configuration is located in `/etc/exabgp/exabgp.conf`.

These configurations can be used as a template:

=== "Single Neighbor"

    A simple configuration for a single neighbor:

    ```c
    # Define the ExaCheck process
    process exacheck {
        run exacheck run;
        encoder text;
    }

    # Connect to the BGP neighbor 192.0.2.1
    neighbor 192.0.2.1 {
        description "Example BGP neighbor";

        # This should be set to the ExaBGP router ID (eg. the main IP address of this server)
        router-id 192.0.2.10;

        # The local address to source BGP connections from
        local-address 192.0.2.10;

        # The local and peer AS numbers
        local-as 65515;
        remote-as 65515;

        # The address family to advertise
        family {
            ipv4 unicast;
        }

        # Allow routes sent from the ExaCheck process to be sent to this neighbor
        api {
            processes [ exacheck ];
        }
    }
    ```

=== "Multiple Neighbor"

    A configuration file for multiple neighbors:

    ```c
    # Define the ExaCheck process
    process exacheck {
        run exacheck run;
        encoder text;
    }

    # Define a template to apply common configuration to neighbors
    template common {
        # This should be set to the ExaBGP router ID (eg. the main IP address of this server)
        router-id 192.0.2.10;

        # The local address to source BGP connections from
        local-address 192.0.2.10;

        # The local and peer AS numbers
        local-as 65515;
        remote-as 65515;

        # The address family to advertise
        family {
            ipv4 unicast;
        }

        # Allow routes sent from the ExaCheck process to be sent to these neighbors
        api {
            processes [ exacheck ];
        }
    }

    # Connect to the BGP neighbor 192.0.2.1
    neighbor 192.0.2.1 {
        description "Example BGP neighbor";
        inherit common;
    }

    # Connect to the BGP neighbor 192.0.2.2
    neighbor 192.0.2.2 {
        description "Example BGP neighbor";
        inherit common;
    }
    ```

=== "Multiple Address Families"

    This configuration can be used for advertising routes to both IPv4 and IPv6 neighbors:

    ```c
    # Define the ExaCheck process
    process exacheck {
        run exacheck run;
        encoder text;
    }

    # Define a template to apply common configuration to IPv4 neighbors
    template common-ipv4 {
        # This should be set to the ExaBGP router ID (eg. the main IP address of this server)
        router-id 192.0.2.10;

        # The local address to source BGP connections from
        local-address 192.0.2.10;

        # The local and peer AS numbers
        local-as 65515;
        remote-as 65515;

        # The address family to advertise
        family {
            ipv4 unicast;
        }

        # Allow routes sent from the ExaCheck process to be sent to these neighbors
        api {
            processes [ exacheck ];
        }
    }

    # Define a template to apply common configuration to IPv6 neighbors
    template common-ipv6 {
        # This should be set to the ExaBGP router ID (eg. the main IP address of this server)
        router-id 192.0.2.10;

        # The local address to source BGP connections from
        local-address 2001:db8::a;

        # The local and peer AS numbers
        local-as 65515;
        remote-as 65515;

        # The address family to advertise
        family {
            ipv6 unicast;
        }

        # Allow routes sent from the ExaCheck process to be sent to these neighbors
        api {
            processes [ exacheck ];
        }
    }

    # Connect to the BGP neighbor 192.0.2.1
    neighbor 192.0.2.1 {
        description "Example IPv4 BGP neighbor";
        inherit common-ipv4;
    }

    # Connect to the BGP neighbor 2001:db8::1
    neighbor 2001:db8::1 {
        description "Example IPv6 BGP neighbor";
        inherit common-ipv6;
    }
    ```

## ExaCheck Configuration

These are some example ExaCheck configuration files with various features used. By default the configuration file is located at `/etc/exabgp/exacheck.yaml`.

=== "Basic Configuration"

    A basic HTTP health check configuration; logging is only to STDOUT:

    ```yaml
    ---
    # The list of health checks to perform
    checks:

    --8<--
    examples/checks/http/basic.md
    --8<--
    ```

=== "Notifications/Logging Configuration"

    Multiple health checks configured with notifications to Microsoft Teams and file logging:

    ```yaml
    ---

    # Configure logging
    logging:

    --8<--
    examples/logging/file/basic.md
    --8<--

    # Configure notifications
    notifications:

    --8<--
    examples/notifications/teams.md
    --8<--

    # The list of health checks to perform
    checks:

    --8<--
    examples/checks/http/basic.md
    --8<--

    --8<--
    examples/checks/ntp/stratum.md
    --8<--

    --8<--
    examples/checks/dns/cname-check.md
    --8<--
    ```

[ExaCheck Configuration - Health Checks]: ../configuration/health-checks/index.md
[ExaBGP GitHub]: https://github.com/Exa-Networks/exabgp
