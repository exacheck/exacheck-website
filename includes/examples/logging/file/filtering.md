  # File logging with filtering applied for events and checks
  # Only announce and withdraw events will be logged
  - method: file
    destination: /tmp/exacheck-announcements.log
    size: 1MB
    count: 10
    events:
      - announce
      - withdraw
    checks:
      - Example Check 1
      - Example Check 2
