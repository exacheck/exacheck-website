  - name: Example HTTP Check with POST data
    description: Send a HTTP POST request to a web server
    args:
      method: http
      host: 192.0.2.50
      url: https://www.example.com/submit.php
      verify_ssl: true
      request_method: POST
      data:
        field1: First field of data
        field2: Another field of data
    prefixes:
      - 192.0.2.240/32
      - 192.0.2.0/29
    nexthop: 192.0.2.50
