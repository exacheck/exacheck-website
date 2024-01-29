  - name: Example DNS CNAME Test
    description: Perform a CNAME query for www.example.com to 192.0.2.1 and verify the CNAME target contains the word "example"
    args:
      method: dns
      host: 192.0.2.1
      query: www.example.com
      type: cname
      pattern: example
    prefixes:
      - 192.0.2.253
    nexthop: self
