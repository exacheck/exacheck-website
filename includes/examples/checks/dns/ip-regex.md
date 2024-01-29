  - name: DNS query with IP regex and neighbor filtering
    description: >
      Send an A query for "example.com" to 192.0.2.1 and ensure the response contains the IP address 192.0.2.250 using a regex.
      The routes to advertise will be filtered to specific neighbors.
    args:
      method: dns
      host: 192.0.2.1
      query: example.com
      query_type: a
      response: ^192\.0\.2\.250$
    nexthop: 192.168.0.3
    prefixes:
      - 192.0.2.2
      - 192.0.2.3
    neighbors:
      - 192.0.2.230
      - 192.0.2.231
      - 192.0.2.232
