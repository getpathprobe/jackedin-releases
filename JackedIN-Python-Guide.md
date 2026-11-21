# JackedIN Python guide

JackedIN already speaks `jackedin exec`, dry-run, and YAML expect rules. The Python package calls that program instead of opening a second SSH stack. A script keeps the same prompt handling, paging, and commit-confirmed plan as the terminal.

## Install

Install from PyPI. You need JackedIN 1.2.0 installed, and Python 3.9 or newer (3.10 or newer for Nornir).

```bash
pip install jackedin
```

For Nornir, install `jackedin` first, then:

```bash
pip install nornir-jackedin
```

The same wheels are also on the JackedIN 1.2.0 release:

```bash
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/jackedin-1.2.0-py3-none-any.whl
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/nornir_jackedin-1.2.0-py3-none-any.whl
```

Check a release-URL install against `SHA256SUMS` on the same release. The pytest helpers (`assert_matches`, the `jackedin_expect` fixture) also need `pip install pytest`.

Set `JACKEDIN_BIN` to the `jackedin` program when it is not on `PATH`. On Windows that is `jackedin.com` from the portable zip, or the installed copy.

## What it costs

The Python packages are free. They drive your JackedIN app, so the app's 72-hour trial or a JackedIN license is needed, the same as the terminal. Run, dry-run, expect rules, saved sessions, the commit-confirmed plan, the Netmiko-style adapter, the Nornir plugin, and the pytest helpers have no extra charge.

Tested on real Juniper hardware before release.

## Why

- One engine for the window, the command line, and Python.
- `dry_run` prints the commands and does not connect.
- Expect rules are the same YAML file the command line reads.
- A password is `JACKEDIN_PASSWORD` or `--password-stdin`. It is never an argument and never logged.
- `JackedinDevice` matches `send_command` and `send_config_set` closely enough that a Netmiko-style script can switch the class.
- `nornir-jackedin` is a Nornir connection and three tasks, for inventories that already use Nornir. Nornir needs Python 3.10 or newer.

## Run a show command

The host is documentation address `192.0.2.10`. The user is `netops`.

```python
from jackedin import Jackedin

device = Jackedin("192.0.2.10", username="netops")
report = device.run(["show version"])
print(report.commands[0].output)
```

`connect` is the same call. `jackedin exec` connects, runs the commands, and disconnects.

A saved session uses the session name, not a secret:

```python
device = Jackedin.from_session("router1")
```

## Dry-run

```python
plan = device.dry_run(["show version"])
assert plan.sent is False
print(plan.commands)
```

No password is sent. The plan text says the command was not connected.

## Expect rules

```python
rules = """
- command: show version
  expect_match: Version
  expect_no_match: "% Invalid"
"""
report = device.run(["show version"], expect=rules)
```

A file that contains `password:` or `secret:` is rejected before it is written.

## Commit confirmed

```python
print(device.commit_confirmed(minutes=5).text)
```

This prints `commit confirmed 5`, the confirm commands, and the rollback. Nothing is sent. Cisco prints `configure replace` guidance instead of a Junos commit. `confirm()` and `rollback()` print those steps only.

## Serial username

SSH and Telnet default the user to `netops`. A serial session does not pass `--user` unless you set `username`:

```python
console = Jackedin("COM5", protocol="serial")
```

JackedIN 1.2.0 does not answer a bare `Password:` prompt when `--user` is set. A fix is planned for the next JackedIN update. Until then, leave `username` unset on a password-only console.

## Junos configuration

`send_config_set` on Junos uses `configure private`. By default it then runs `rollback 0` and `exit`, so the shared candidate is untouched and `exit` does not fail with uncommitted changes. Nothing is committed.

```python
device.send_config_set(["set system host-name router1"], commit=True, commit_minutes=5)
```

`commit=True` uses `configure exclusive` and `commit confirmed`. Junos rejects commit confirmed inside a private session. That run also sends `rollback 0` and `exit`, and it passes `--no-stop-on-error`, so a failed line or a failed commit still clears the candidate and releases the exclusive lock. `rollback 0` after a successful commit confirmed reloads that commit. It does not cancel the confirm timer. Cisco has no commit confirmed, so `commit=True` is refused there.

## Enable mode

Cisco consoles often land at `router>`. Pass the enable secret as `enable` or `secret`. The library sets `JACKEDIN_ENABLE_PASSWORD` on the child process and passes `--enable-password-env JACKEDIN_ENABLE_PASSWORD`. The value is not an argument and it is not logged.

When that secret is set, `enable` is sent once at the start of the command list on a Cisco session, and on a serial session that has no vendor. That covers `show startup-config`, `write`, `copy`, `debug`, `show privilege`, and `reload`, not only `show running-config`. Nothing is prepended when no secret was given. Junos does not get an `enable` command.

```python
device = Jackedin("COM5", protocol="serial", vendor="cisco", enable=enable_secret)
device.run(["show running-config"])
```

Nornir uses the same value as a connection extra named `enable` or `secret`.

## Logout and expect rules

Do not end a command list with `exit`, `logout`, or `quit` when expect rules are set. The library refuses that call. After a logout the console is back at `login:`, and an expect check must not be typed there. The next JackedIN update will also stop sending once `login:`, `Username:`, or `Password:` returns, and score the rules against output already captured. JackedIN 1.2.0 does not have that stop yet, so the library refuses the call instead.

## Expect dicts

```python
device.run(["show version"], expect=[{"command": "show version", "expect_match": "Version"}])
```

A YAML string and `ExpectRule` values also work. Another shape raises `UsageError`.

## Netmiko-style calls

```python
from jackedin import Jackedin, JackedinDevice

device = JackedinDevice(Jackedin("192.0.2.10", username="netops", vendor="cisco"))
print(device.send_command("show version"))
print(device.send_config_set(["hostname router1"]))
device.disconnect()
```

`send_config_set` enters configuration mode and leaves it. It does not commit. Call `commit_confirmed` when you want the printed plan.

## Nornir

```bash
pip install nornir-jackedin
```

```python
from nornir.core.plugins.connections import ConnectionPluginRegister
from nornir_jackedin.plugins.tasks import jackedin_send_command

ConnectionPluginRegister.auto_register()
# nr is your Nornir object. The host in examples is 192.0.2.10, user netops.
result = nr.run(task=jackedin_send_command, command="show version")
```

`jackedin_commit_confirmed` returns the plan and sets `changed` false.

## pytest

```python
from jackedin import assert_matches

def test_router_config():
    captured = "hostname router1\n"
    assert_matches(captured, "- command: show running-config\n  expect_match: hostname router1\n")
```

With the package installed, pytest provides `jackedin_expect`. The check uses the string you already captured. It does not dial the device.

## Notebook

`jackedin.ipynb` in `jackedin-python-examples-1.2.0.zip` (on the same release) walks through dry-run, expect rules, and the commit plan with the same placeholders. Run it only against a lab device you are allowed to test. The cells as written call `dry_run` and `commit_confirmed`, which do not connect.

A short script, `python-recipe.py`, is in the same zip.

## Troubleshooting

- `JackedIN did not return JSON.`: run `jackedin license status`. When the 72-hour trial has ended, JackedIN refuses the command and the 1.2.0 library shows this short message. A clearer message is planned for the next update. Enter your license with `jackedin license activate`.
- `jackedin` not found: set `JACKEDIN_BIN` to the full path of the program.
- `ModuleNotFoundError: No module named 'pytest'` when importing `assert_matches`: install pytest. Plain `import jackedin` does not need it.
