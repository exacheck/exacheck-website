  - name: Example ICMP Latency Check
    description: Ensure that ICMP ping requests to the IP 192.0.2.1 have a latency below 20ms across 5 pings
    args:
      method: icmp
      host: 192.0.2.1
      count: 5
      max_latency: 20
    prefixes:
      - 192.0.2.5
    nexthop: 192.0.2.254
