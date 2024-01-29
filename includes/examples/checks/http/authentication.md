  - name: Example HTTP Check with Authentication
    description: Perform a HTTP request which requires basic authentication
    args:
      method: http
      host: 127.0.0.1
      url: https://user:password@example.com
      verify_ssl: true
      expected_status: 200
    prefixes:
      - 2001:db8::ffff/128
    nexthop: self
