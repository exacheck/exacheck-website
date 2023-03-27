---
title: CLI
description: Usage of the ExaCheck command line interface.
layout: page
nav_order: 40
permalink: /cli.html
---

# ExaCheck CLI
{: .no_toc }

A command line interface is supplied to run ExaCheck: `exacheck`

## Table of Contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Basic Usage

To see the available options run `exacheck` with the `--help` flag:

```bash
exacheck --help
```

By default logs are output to STDERR with the log level set to warning; to raise the log level use the `-v` flag one or more times with the command you are running:

```bash
exacheck run -vvvvvv
```

## CLI Run Command

The `run` command is used to execute ExaCheck. The following arguments are available:

- `--file [filename] | -f [filename]`: The path to the [configuration file][ExaCheck Configuration File]. The default file is `/etc/exabgp/exacheck.yaml`.

### Example Run Command Usage

```bash
# Usual usage
exacheck run

# With debugging and loading an alternative configuration file
exacheck run -f /tmp/exacheck.yaml -vvvvvv
```

## CLI Test Command

The `test` command is used to load and validate a configuration file. Any configuration errors will be reported. This may be used with automation tools that build the configuration file to test that it is working/valid before actual deployment.

The following arguments are available:

- `--file [filename] | -f [filename]`: The path to the [configuration file][ExaCheck Configuration File]. The default file is `/etc/exabgp/exacheck.yaml`.

### Example Test Command Usage

```bash
# Test default configuration
exacheck test

# With debugging and loading an alternative configuration file
exacheck test -f /tmp/exacheck.yaml -vvvvvv
```

## CLI Schema Command

The `schema` command is used to dump the configuration file JSON schema to STDOUT. See the [configuration schema][ExaCheck Configuration File Schema] section for more details.

### Example Schema Command Usage

```bash
# Output configuration schema to /tmp/schema.json
exacheck schema > /tmp/schema.json
```

[ExaCheck Configuration File]: /configuration/basics.html
[ExaCheck Configuration File Schema]: /configuration/basics.html#configuration-schema