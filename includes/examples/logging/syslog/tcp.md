  # Send logs for announce/withdraw events using TCP to 192.0.2.100 port 514
  - method: syslog
    destination: 192.0.2.100
    protocol: tcp
    events:
      - announce
      - withdraw
