  - name: Example ICMP Latency + Packet Loss Check
    description: Ensure that ICMP ping requests to the IP 2001:db8:ffff::5 have a latency below 250ms but allow up to 50% packet loss
    args:
      method: icmp
      host: 2001:db8:ffff::5
      count: 4
      max_latency: 250
      max_loss: 2
    prefixes:
      - 2001:db8:a::/64
    nexthop: self
