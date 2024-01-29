  - name: Example Basic Shell Check
    description: Run the command "true" (will always return exit code 0)
    args:
      method: shell
      command: true
    prefixes:
      - 192.0.2.255
    nexthop: self
