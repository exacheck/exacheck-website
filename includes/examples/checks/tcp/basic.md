  - name: Example TCP Check
    description: Ensure that the IP 192.0.2.80 responds on port 80
    args:
      method: ntp
      host: 192.0.2.80
      port: 80
    prefixes:
      - 192.0.2.0/29
    nexthop: self
