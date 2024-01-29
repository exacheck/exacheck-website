---
icon: material/text-long
---

# File

The `file` log method can be used to send logs to a file. By default logs will be rotated and compressed to ensure the disk doesn't get filled up.

## Configuration Keys

The following configuration keys apply to only the file target. The [logging page][ExaCheck Configuration - Logging] lists general configuration which is shared with the `syslog` logger.

| Key                                         | Type    | Default             |
| ------------------------------------------- | ------- | ------------------- |
| [`structured`](#structured)                 | Bool    | `False`             |
| [`destination`](#destination)               | String  | `/tmp/exacheck.log` |
| [`size`](#size)                             | String  | `10MB`              |
| [`count`](#count)                           | Integer | `5`                 |
| [`compress`](#compress)                     | Bool    | `True`              |
| [`compression_format`](#compression-format) | String  | `gz`                |

### Structured

--8<--
snippets/logging/structured.md
--8<--

### Destination

The path to the log file. During startup the path is checked to ensure that the ExaCheck process can write to it.

### Size

The maximum log file size before rotating the log file. Defaults to `10MB`. Values can be specified in the format `<size><unit>`.

### Count

The maximum number of rotated log files to keep.

### Compress

The `compress` option allows for compression of rotated log files. If disabled, rotated logs will not be compressed.

#### Compression Format

The `compression_format` option specifies which format to use for log file compression. The list of valid options are:

- `gz`
- `bz2`
- `xz`
- `lzma`
- `tar`
- `tar.gz`
- `tar.bz2`
- `tar.xz`
- `zip`

By default `gz` is used as it is most commonly available.

## Examples

These are some examples of what can be configured for the `file` target.

=== "Basic File Log"

    A bare minimum configuration for logging to a file:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/file/basic.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

=== "Filtered File Log"

    Logging to a file with filtering applied:

    ```yaml
    ---

    logging:

    --8<--
    examples/logging/file/filtering.md
    --8<--

    --8<--
    examples/check_footer.md
    --8<--
    ```

[ExaCheck Configuration - Logging]: index.md
