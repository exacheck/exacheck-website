---
icon: octicons/command-palette-24
description: Usage instructions for the ExaCheck CLI to run ExaCheck, validate the configuration and dump the configuration schema.
---

# Command Line Interface

A command line interface `exacheck` is included with ExaCheck. The CLI allows you to run ExaCheck, dump the JSON configuration schema and validate the configuration file.

## Running ExaCheck

To run ExaCheck use the `run` command:

```bash
exacheck run
```

By default, the configuration will attempt to be loaded from the file `/etc/exabgp/exacheck.yaml`.

### Run Options

The following options are available for the `run` command:

| Option Name          | Type   | Description                                                          |
| -------------------- | ------ | -------------------------------------------------------------------- |
| `-h` / `--help`      | Flag   | Show the help output and exit.                                       |
| `-f` / `--file`      | String | The path to the configuration file to load from.                     |
| `-v` / `--verbosity` | Count  | The verbosity level. May be specified multiple times (eg. `-vvvvv`). |

### Run Environment Variables

The following environment variables are supported:

| Variable Name        | Type    | Description                                  |
| -------------------- | ------- | -------------------------------------------- |
| `EXACHECK_CONFIG`    | String  | The path to the configuration file to load.  |
| `EXACHECK_VERBOSITY` | Integer | The verbosity level (higher is more verbose) |

## Testing Configuration

The `test` command can be used to load and validate the configuration file. The test command is a no-op; logs/notifications will not be sent to any defined targets except STDOUT.

To test the configuration:

```bash
exacheck test
```

To enable verbose output:

```bash
exacheck test -vvvvvv
```

### Testing Options

The following options are available for the `test` command:

| Option Name          | Type   | Description                                                          |
| -------------------- | ------ | -------------------------------------------------------------------- |
| `-h` / `--help`      | Flag   | Show the help output and exit.                                       |
| `-f` / `--file`      | String | The path to the configuration file to load from.                     |
| `-v` / `--verbosity` | Count  | The verbosity level. May be specified multiple times (eg. `-vvvvv`). |

### Test Environment Variables

The following environment variables are supported:

| Variable Name        | Type    | Description                                   |
| -------------------- | ------- | --------------------------------------------- |
| `EXACHECK_CONFIG`    | String  | The path to the configuration file to load.   |
| `EXACHECK_VERBOSITY` | Integer | The verbosity level (higher is more verbose). |

## Configuration Schema

The `schema` command is used to generate the JSON schema file. The JSON schema will be printed to STDOUT where you can then redirect it into a file if needed. As an example:

```bash
exacheck schema > schema.json
```

The JSON schema file can in turn be used to validate the configuration and provide hints to editors that support it (eg. VS Code).
