  - name: Example Script With Environment Variables
    description: Run a script with environment variables
    args:
      method: shell
      command: /path/to/script.py
      environment:
        EXAMPLE: example environment variable 1
    prefixes:
      - 192.0.2.230
    nexthop: 192.0.2.1
