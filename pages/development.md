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
- [mypy][mypy] for static type checking
- [Flake8][Flake8] and [Pylint][Pylint] for linting
- f strings used for variable interpolation

The recommended way of editing the code is using VS Code with the development container (see below) which includes the relevant extensions and Python modules.

### Logging

[Loguru][Loguru] is used for logging with logging contexts used to prepend the process ID and task name to log messages. To log messages `self.log` should be called rather than `logger` otherwise the context will be wrong.

Log messages are formatted in lazy mode; any log messages with variables/functions should be logged using replacement f strings:

```python
self.log.info(
    "Some message with a variable: {some_variable}",
    some_variable="An example variable",
)
```

## Development Container

To allow easy development a [development container][ExaCheck Development Container] is included for use with VS Code. The development container will install Python (in a [conda][Conda] environment). Various extensions are installed with the development container for linting Python code, formatting Python code and more.

To use the container you must have:

- [VS Code][VS Code]
- [Docker][Docker]
- [VS Code Remote Development Extension][VS Code Remote Development Extension]
- [VS Code Dev Containers Extension][VS Code Dev Containers Extension]

For further information see the official [remote extension documentation][VS Code Remote Extension Docs] and [development container documentation][Development Containers Docs].

[ExaCheck Development Container]: https://github.com/exacheck/exacheck/blob/main/.devcontainer
[Conda]: https://docs.conda.io/en/latest/
[VS Code]: https://code.visualstudio.com/
[Docker]: https://www.docker.com/
[VS Code Remote Development Extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack
[VS Code Dev Containers Extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[VS Code Remote Extension Docs]: https://code.visualstudio.com/docs/remote/remote-overview
[Development Containers Docs]: https://code.visualstudio.com/docs/devcontainers/containers
[Black]: https://github.com/psf/black
[mypy]: https://www.mypy-lang.org/
[Flake8]: https://flake8.pycqa.org/en/latest/
[Pylint]: https://github.com/PyCQA/pylint
[Loguru]: https://github.com/Delgan/loguru
