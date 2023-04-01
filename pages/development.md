---
title: Development
description: ExaCheck development and contribution information.
layout: page
nav_order: 50
permalink: /development.html
---

# ExaCheck Development
{: .no_toc }

Looking to contribute to ExaCheck or modify it for your requirements? See below.

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Coding Style

The current code follows these standards:

- Formatted with [black][Black] with a configured line length maximum of 120
- [f-strings][Python f-strings] used for variable interpolation
- [Flake8][Flake8] and [Pylint][Pylint] for linting
- [MyPy][MyPy] for static type checking

The recommended way of editing the code is using VS Code with the [development container](#development-container) which includes the relevant extensions and Python modules.

### Logging

[Loguru][Loguru] is used for logging with logging contexts used to append the check name and other information to log messages. When calling custom checks, a logging context should be passed to the check (`self.log`). To log messages the following values must be bound:

- `check_name` - Should be set by the logging context for the check
- `subsystem` - The [name of the subsystem][ExaCheck Logging Configuration - Subsystems] sending the log message
- `event` - The [type of event][ExaCheck Logging Configuration - Events] sending the log message

Variables should be formatted using f-string style replacements.

A typical example of sending a log message:

```python
self.log.bind(subsystem="healthcheck", event="debug").info(
    "Some message with a variable: {some_variable}",
    some_variable="An example variable",
)
```

If logging a message that calls a function, it is recommended to set the `lazy` option for the log. This will only call the function for the log message if required (eg. if the log level would skip the message, the function would not be called at all). To do this the function should be a callable object (eg. use a `lambda`):

```python
self.log.bind(subsystem="healthcheck", event="debug").opt(lazy=True).info(
    "Some message with a function: {some_function}",
    some_function=lambda: self.some_function(),
)
```

## Health Checks

Health check classes are developed with at least two methods:

- `__init__`: The health check is configured. No actual check should be executed on init.
- `check`: The actual health check method. The method is called each health check iteration without arguments. The health check must return a `CheckResult` object which contains the result of the check and any error, exception or log messages.

The health check class init method only gets called once on startup of the worker. The init method must not perform any steps that may impact the subsequent health checks. Examples of things **not to do**:

- Resolve a hostname to an IP address: If the IP address for the hostname changes the health check won't know about it until its restarted.
- Test if a file/directory exists which the health check relies on.

## Development Container

To allow easy development a [development container][ExaCheck Development Container] is included for use with VS Code. The development container will install Python (in a [conda][Conda] environment). Various extensions are installed with the development container for linting Python code, formatting Python code and more.

To use the container you must have:

- [Docker][Docker]
- [VS Code Dev Containers Extension][VS Code Dev Containers Extension]
- [VS Code Remote Development Extension][VS Code Remote Development Extension]
- [VS Code][VS Code]

For further information see the official [remote extension documentation][VS Code Remote Extension Docs] and [development container documentation][Development Containers Docs].

[Black]: https://github.com/psf/black
[Conda]: https://docs.conda.io/en/latest/
[Development Containers Docs]: https://code.visualstudio.com/docs/devcontainers/containers
[Docker]: https://www.docker.com/
[ExaCheck Development Container]: https://github.com/exacheck/exacheck/blob/main/.devcontainer
[ExaCheck Logging Configuration - Subsystems]: /configuration/logging.html#log-subsystems
[ExaCheck Logging Configuration - Events]: /configuration/logging.html#log-events
[Flake8]: https://flake8.pycqa.org/en/latest/
[Loguru]: https://github.com/Delgan/loguru
[MyPy]: https://www.mypy-lang.org/
[Pylint]: https://github.com/PyCQA/pylint
[Python f-strings]: https://peps.python.org/pep-0498/
[VS Code Dev Containers Extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[VS Code Remote Development Extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack
[VS Code Remote Extension Docs]: https://code.visualstudio.com/docs/remote/remote-overview
[VS Code]: https://code.visualstudio.com/
