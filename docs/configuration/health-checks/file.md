---
icon: material/file
description: The ExaCheck file health check tests for the existence or absence of a file to determine if a service is healthy.
---

# File

The `file` health check can verify that either a file exists or doesn't exist.

## Configuration Keys

The following configuration options apply to the file health check method:

| Key                 | Type   | Default |
| ------------------- | ------ | ------- |
| [`path`](#path)     | String | *undef* |
| [`exists`](#exists) | Bool   | `True`  |

### Path

The path to the file to test for.

### Exists

If `exists` is set to `True` (the default), the file path must exist for the health check to return success. If set to `False`, the file path must not exist for the health check to return success.

## Examples

These are some configuration examples for the file health check:

=== "File Exists"

    To verify that a file exists:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/file/basic.md
    --8<--
    ```

=== "File Does Not Exist"

    To verify that a file does not exist:

    ```yaml
    ---

    # The list of health checks
    checks:

    --8<--
    examples/checks/file/not-exists.md
    --8<--
    ```
