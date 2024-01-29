  - name: Example Basic ICMP Check
    description: Ensure that the IP 8.8.8.8 responds to ICMP ping requests
    args:
      method: icmp
      host: 8.8.8.8
    prefixes:
      - 192.0.2.255
    nexthop: self
