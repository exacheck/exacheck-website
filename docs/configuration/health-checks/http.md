---
icon: material/web
description: The ExaCheck HTTP health check validates that a web server responds to a request of the chosen method. Optionally the SSL certificate can be checked to ensure it is trusted.
---

# HTTP

The `http` health check allows you to perform HTTP/HTTPS requests to a web server. To verify the service is working correctly there are options to send POST data, validate the response code, testing the response content and validating the SSL.

## Configuration Keys

The following configuration options apply to the DNS health check method:

| Key                                   | Type               | Default                                   |
| ------------------------------------- | ------------------ | ----------------------------------------- |
| [`url`](#url)                         | String             | *undef*                                   |
| [`response`](#response)               | *Optional* Pattern | *undef*                                   |
| [`expected_status`](#expected-status) | *Optional* Integer | *undef*                                   |
| [`require_status`](#require-status)   | Bool               | `True`                                    |
| [`http_timeout`](#http-timeout)       | Integer            | `5`                                       |
| [`user_agent`](#user-agent)           | String             | `ExaCheck HTTP Health Check [v<version>]` |
| [`headers`](#headers)                 | *Optional* Dict    | *undef*                                   |
| [`verify_ssl`](#verify-ssl)           | Bool               | `False`                                   |
| [`request_method`](#request-method)   | String             | `GET`                                     |
| [`data`](#data)                       | *Optional* Dict    | *undef*                                   |

### Remote Check Options

As this is a remote check, the following additional options are supported:

--8<--
snippets/checks/remote-args.md
--8<--

### URL

The full URL to request from the web server. The actual HTTP request is sent to the web server defined in the `host` variable with the host header in the HTTP request being set to the value from the URL.

HTTPS requests use SNI.

If basic authentication is required the username/password can be added to the URL (eg. `http://user:password@example.com`) or the `headers` option can be used.

### Response

The `response` value may be set to a pattern to match the content returned from the web server. If not set (the default) no checks are performed on the actual content returned by the web server.

### Expected Status

The `expected_status` code may be set to ensure that the web server responds with a specific HTTP status code. In some cases you may want to validate the web server responds with a specific status code (eg. `301`) and not just a `200`.

### Require Status

When the `require_status` option is set to `True` (the default), the HTTP response code must indicate that the request was successful. If `expected_status` is set to a non-successful response code this setting is overridden.

### HTTP Timeout

The `http_timeout` option determines how long the HTTP request is allowed to wait for a response.

### User Agent

The default user agent header can be overridden by setting the `user_agent` value to a custom value.

### Headers

If additional headers are required to be sent with the HTTP request a dict of the headers may be provided. As an example:

```yaml
      headers:
        Example-Header: Example-Data
        Another-Header: More-Data
```

### Verify SSL

Set `verify_ssl` to `True` to validate that the SSL certificate is trusted by the systems certificate store.

### Request Method

By default the HTTP check will make a `GET` request to the web server. The `request_method` may be set to one of the following values:

- `GET`
- `POST`
- `PUT`
- `DELETE`
- `HEAD`
- `OPTIONS`

### Data

If the `request_method` is set to a value that allows data to be included (eg. `POST` requests), a dict of data can be set. As an example:

```yaml
      request_method: POST
      data:
        field1: example
        field2: another example
```

## Examples

Some examples of HTTP health checks:

=== "Basic"

    A basic configuration:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/http/basic.md
    --8<--
    ```

=== "DNS Name"

    A basic configuration using a hostname as the `host` to connect to:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/http/dns-name.md
    --8<--
    ```

=== "Basic Authentication"

    A HTTP check that requires basic authentication:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/http/authentication.md
    --8<--
    ```

=== "POST Data"

    A HTTP check which includes POST data:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/http/post.md
    --8<--
    ```
