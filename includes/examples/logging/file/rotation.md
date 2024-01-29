  # File logger with rotation configured
  - method: file
    destination: /tmp/exacheck.log
    level: info
    # Only log events from "Example Check 1"
    checks:
      - Example Check 1
    # Rotate log file once it reaches 20MB
    size: 20MB
    # Keep 5 log files
    count: 5
    # Compress the rotated logs
    compress: true
