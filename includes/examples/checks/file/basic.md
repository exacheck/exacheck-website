  - name: Example file exists check
    description: Verify that the file path "/var/run/exists" exists
    args:
      method: file
      path: /var/run/exists
    prefixes:
      - 192.0.2.255
    nexthop: self
