---
icon: material/bash
description: The ExaCheck shell health check runs the specified command in a shell session and verifies that the exit code indicates success.
---

# Shell

The `shell` health check allows you to run a command and validate the response code is expected. This check method can be used to run your own custom scripted health checks easily.

## Configuration Keys

The following configuration options apply to the file health check method:

| Key                           | Type            | Default |
| ----------------------------- | --------------- | ------- |
| [`command`](#command)         | String          | *undef* |
| [`environment`](#environment) | *Optional* Dict | *undef* |

### Command

The `command` needs to be set to the command that should be executed.

### Environment

The `environment` parameter can be used to set custom environment variables used by the script/command that needs to be executed. The variables should be specified as key/values.

## Examples

Some examples of shell health checks:

=== "Basic"

    A basic configuration:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/shell/basic.md
    --8<--
    ```

=== "Environment Variables"

    An example of running a script with environment variables:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/shell/environment.md
    --8<--
    ```
