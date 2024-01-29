  - name: Example Basic NTP Check
    description: Ensure that the IP 192.0.2.123 responds to NTP queries
    args:
      method: ntp
      host: 192.0.2.123
    prefixes:
      - 192.0.2.255
    nexthop: self
