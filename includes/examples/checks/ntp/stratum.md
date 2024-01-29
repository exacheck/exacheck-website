  - name: Example NTP Stratum Check
    description: Ensure that the IP 2001:db8::123 responds to NTP queries and the server is at least stratum 2
    args:
      method: ntp
      host: 2001:db8::123
      max_stratum: 2
    prefixes:
      - 2001:db8:aaaa::ffff/128
      - 2001:db8:aaaa::123/128
    nexthop: self
