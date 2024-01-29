  - name: Example Basic HTTP Check
    description: >
      Perform a HTTP request to example.com. The IPv4 address for example.com will be resolved.
      If there are multiple IP addresses available, a response from any is considered successful.
    args:
      method: http
      host: example.com
      url: https://example.com
      address_family: ipv4
      all_valid: false
    prefixes:
      - 192.0.2.255
    nexthop: self
