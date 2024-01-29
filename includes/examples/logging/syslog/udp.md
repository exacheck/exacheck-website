  # Send logs to 192.0.2.1 UDP port 5144
  - method: syslog
    destination: 192.0.2.1
    port: 5144
    protocol: udp
    structured: false
