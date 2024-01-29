  - name: Example DNS Service
    description: Perform a basic SOA query for example.com to 192.0.2.255. If the query returns a response, 192.0.2.255 would be advertised with BGP.
    args:
      method: dns
      host: 192.0.2.255 # Note DNS queries are being sent to 192.0.2.255 which should be bound to loopback
      query: example.com
    prefixes:
      - 192.0.2.255
    nexthop: self
