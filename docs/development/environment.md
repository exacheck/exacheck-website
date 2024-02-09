---
icon: material/microsoft-visual-studio-code
description: Instructions for using the included Visual Studio Code development environment in a Docker container.
---

# Development Environment

If using VS Code, a [development environment][ExaCheck Development Environment] is available. The development environment includes everything needed for editing, testing and linting.

## Requirements

The following requirements are needed to use the development environment:

- [Visual Studio Code][Visual Studio Code]
- [Visual Studio Code Dev Containers extension][Code Extension: Dev Containers]
- [Docker][Docker: Get Docker] - Only the [Docker Engine][Docker: Install Docker Engine] package is required for Linux

## Instructions

First make sure the [requirements](#requirements) are installed.

Clone the ExaCheck repository:

=== "SSH Transport"

    ```bash
    git clone git@github.com:exacheck/exacheck.git
    ```

=== "HTTPS Transport"

    ```bash
    git clone https://github.com/exacheck/exacheck.git
    ```

In VS Code, go to File -> Open Workspace from File. You can then browse to the repository that was cloned and select the `exacheck.code-workspace` file.

VS Code will then prompt you to reopen the workspace in the development container. The development container will then be pulled. The VS Code extensions will be automatically install inside the development container.

On container creation the [create.sh][ExaCheck Development Environment: create.sh] script will be executed. This script will install all Python modules required using Poetry.

[ExaCheck Development Environment]: https://github.com/exacheck/exacheck/tree/main/.devcontainer
[Visual Studio Code]: https://code.visualstudio.com/
[Code Extension: Dev Containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[Docker: Get Docker]: https://docs.docker.com/get-docker/
[Docker: Install Docker Engine]: https://docs.docker.com/engine/install/
[ExaCheck Development Environment: create.sh]: https://github.com/exacheck/exacheck/blob/main/.devcontainer/code/scripts/create.sh
