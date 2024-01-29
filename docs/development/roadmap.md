---
icon: material/map
---

# Roadmap

ExaCheck is currently work in progress as I have time. When I started writing ExaCheck I got about half way before taking a break for a few months; at some point I plan to go through everything in more detail to fix up anything I may have forgotten about.

## Upcoming Features

As I need them I plan to add additional health check methods. Unless there is a request or I need it myself you may not have a health check method suitable for your use case. If that is the case please create a request on GitHub; I am interested to see other use cases.

### General Features

- [ ] Complete test files: Currently there is only a basic test for loading the configuration.
- [ ] Logging for when ExaCheck is shut down. Due to a race condition Loguru is not able to log inside a signal handler.
- [ ] Make the `metric_down` feature work. If set, routes should be announced when the service is down but have the configured metric attribute set.

### CLI

- [ ] Command line option to print table of available configuration options using the available field data.
- [ ] Command line option to send test notifications.
- [ ] Option to list available checks and their configuration (or view configuration for a single check.)

### Shell Health Check

- [ ] Add variable support to allow passing information to the command that is being executed such as the next hop address.

### HTTP Health Check

- [ ] Add support for HTTP2 and HTTP3.

### DNS Health Check

- [ ] Add support for DNS over TLS (DoT) and DNS over HTTPS (DoH).

## Future Plans

In the future after any features are complete I plan to do these:

- [ ] Clean up comments: The current functions are mostly missing documentation about parameters that are passed to them.
- [ ] Tidy up logging: I plan to tidy up logging a bit and split log messages into "short" and "long".
- [ ] Website tidy up: The website needs to be reviewed and have grammar fixed up.
