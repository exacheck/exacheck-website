  - name: Example file does not exist check
    description: Verify that the file path "/var/run/not-existing" does not exist
    args:
      method: file
      path: /var/run/not-existing
      exists: false
    prefixes:
      - 2001:db8::/64
    nexthop: self
