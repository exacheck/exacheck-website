  # Log specific check to the socket /var/run/log.socket
  - method: syslog
    destination: /var/run/log.socket
    structured: false
    checks:
      - Example Check 1
