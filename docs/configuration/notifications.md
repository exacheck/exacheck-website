---
icon: material/email-fast
---

# Notifications

Notifications may be configured to alert on route announce and withdraw events as well as other general information from the ExaCheck process. Notifications are handled by [Apprise][Apprise - GitHub] - a list of supported notification providers is listed on the [Apprise Wiki][Apprise - Wiki].

Multiple notification targets may be defined; as an example you may want alerts for a specific service to go to one notification service but alerts for other services to go somewhere else.

## Configuration Keys

Notifications are configured as an array of `Notifications` objects. The following top level configuration keys are available for each object.

| Key                                 | Type                    | Default                                     |
| ----------------------------------- | ----------------------- | ------------------------------------------- |
| [`name`](#name)                     | String                  | *undef*                                     |
| [`description`](#description)       | *Optional* String       | *undef*                                     |
| [`url`](#url)                       | String                  | *undef*                                     |
| [`checks`](#checks)                 | *Optional* List[String] | *undef*                                     |
| [`events`](#events)                 | List[String]            | `["announce", "error", "info", "withdraw"]` |
| [`general_events`](#general-events) | Boolean                 | `False`                                     |

### Name

The name for the notification target. The name is used for logging.

### Description

A description for the notification target. This is not used internally; it can just serve to make the configuration file more readable.

### URL

The notification target URL. The [Apprise GitHub README.md][Apprise - GitHub] includes a list of supported services and their URLs.

### Checks

An optional list of check names for filtering. Only notifications for the supplied check names will be sent to the configured target.

### Events

A list of event types allowed to send notifications to this target. The list of supported events are:

- `announce`: Route announcements.
- `withdraw`: Route withdrawals.
- `error`: General errors encountered. These events require the `general_events` flag to be set to `True`.
- `info`: General information events. These events require the `general_events` flag to be set to `True`.

### General Events

Allow `info` and `error` events to be sent to the notification target. If set to `False` (the default) no `info` or `error` event messages will be sent.

## Examples

The following are some examples of notification targets:

```yaml
---

# The list of notification targets
notifications:

--8<--
examples/notifications/teams.md
--8<--

--8<--
examples/notifications/slack.md
--8<--

--8<--
examples/check_footer.md
--8<--
```

[Apprise - GitHub]: https://github.com/caronc/apprise
[Apprise - Wiki]: https://github.com/caronc/apprise/wiki
