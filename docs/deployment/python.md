---
icon: material/language-python
description: ExaCheck installation steps using the PyPi package or directly from the ExaCheck GitHub repository.
---

# Python

ExaCheck requires a recent version of Python; **Python 3.10 - 3.12 is required**. If you try to run ExaCheck on an earlier release of Python it will not work.

## venv Setup

While not required, it is recommended that ExaCheck is installed in a Python virtual environment. To setup a virtual environment, first ensure that the relevant `python-venv` package is installed for the distribution you are running:

=== "Ubuntu/Debian"

    ```bash
    apt install python3-venv
    ```

=== "Alma/CentOS/RedHat"

    Depending on the release, the venv module may already be installed. If not, install the `python3-virtualenv` package:

    ```bash
    yum install python3-virtualenv
    ```

### venv Creation

To create the virtual environment in `/opt/exacheck`:

```bash
python3 -m venv /opt/exacheck
```

The environment should now be activated before continuing with the PyPi or source installation:

```bash
source /opt/exacheck/bin/activate
```

## PyPI Package

ExaCheck can be installed using `pip` from the [PyPI package repository][ExaCheck PyPI Package Repository]:

```bash
python3 -m pip install exacheck
```

All requirements will be installed automatically.

## Source Build

To install ExaCheck from source you must have the `git` package available. To install from the `main` branch:

```bash
python3 -m pip install git+https://github.com/exacheck/exacheck.git@main
```

To install a specific release, change the `main` branch to the relevant release name. As an example for `v0.0.10`:

```bash
python3 -m pip install git+https://github.com/exacheck/exacheck.git@v0.0.10
```

## Post Installation

After installation, ExaBGP requires some additional setup. Follow the steps on the [ExaBGP setup][ExaBGP Setup] page.

### Logging Directory

If file based logging will be used, the directory to store the logs must exist and be writeable by the user running ExaBGP. As an example, if you would like to log to the directory `/var/log/exacheck`:

```bash
mkdir /var/log/exacheck
chown exacheck:exacheck /var/log/exacheck
```

The relevant logging configuration in the ExaCheck configuration file would look like this:

```yaml
---

# Logging configuration
logging:
  - method: file
    destination: /var/log/exacheck/exacheck.log

--8<--
examples/check_footer.md
--8<--
```

## ExaCheck Configuration

You may now proceed with the ExaCheck configuration. The [example configuration files][ExaCheck Examples] can be used as a template.

[ExaCheck PyPI Package Repository]: https://pypi.org/project/exacheck/
[ExaBGP Setup]: exabgp.md
[ExaCheck Examples]: examples.md
