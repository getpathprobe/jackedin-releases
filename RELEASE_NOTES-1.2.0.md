# JackedIN™ 1.2.0 — What's new

JackedIN 1.2.0 is a terminal for SSH, Telnet, and serial consoles on Windows 10/11, Linux, and Raspberry Pi OS (64-bit). There is no macOS build yet. Trial and license terms are unchanged: a 72-hour trial, then one license is one computer, non-transferable, with one year of updates. Tested on real Cisco IOS and Juniper Junos switches; this build passed a live license check.

**Windows:** a portable zip (`jackedin.exe`; scripts use `jackedin.com`) and a setup installer (`JackedIN_1.2.0_x64-setup.exe`). The installer is not code-signed, so SmartScreen may say “Windows protected your PC”. Choose **More info**, then **Run anyway**.

**Raspberry Pi:** a `.deb`, a portable tarball, and the portable binary on its own, for Raspberry Pi OS 64-bit (arm64).

## What's new in 1.2

- Import saved sessions from PuTTY, SecureCRT, MobaXterm, and SSH config.
- Dry-run and commit-confirm with expect rules, so you can preview a change and require a match before it is committed.
- `fleet` to run the same command across a device list.
- An Ansible collection.
- A CI guide and a credential store.
- `backup` pulls the running-config from Cisco IOS and Juniper Junos, with auto-detect, and `diff` compares backups.
- SFTP.
- NetBox and Nautobot sync, and password-manager logins, included at no extra charge.
- Shell completions.
- The PathProbe hand-off picks the network interface that has the default route.
- `update-check`.
- An MCP server so AI assistants can use JackedIN as a tool.

## Added November 21, 2026: Python packages

The JackedIN app and its downloads above are unchanged. Two Python packages and an examples zip were added to this release:

- `jackedin`: a Python client for the same `jackedin` engine. Run commands, dry-run (does not connect), YAML expect rules, saved sessions, the print-only commit-confirmed plan, and a Netmiko-style `JackedinDevice` with `send_command` and `send_config_set`. Passwords stay in `JACKEDIN_PASSWORD` or go on stdin; they are never on the command line or in a log.
- `nornir-jackedin`: a Nornir connection named `jackedin` and the tasks `jackedin_send_command`, `jackedin_send_config`, and `jackedin_commit_confirmed`.
- pytest helpers: `assert_matches`, `assert_report`, and the `jackedin_expect` fixture check captured output against expect rules without connecting.
- Junos `send_config_set` uses a private candidate and commits nothing by default; `commit=True` uses `configure exclusive` and `commit confirmed`. An enable secret is sent once at the start on Cisco sessions, through an environment variable.

The packages are free. They drive the JackedIN app, so the 72-hour trial or a license is needed, the same as the terminal. Tested on real Juniper hardware; the packages passed a live license check with this release's app.

```sh
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/jackedin-1.2.0-py3-none-any.whl
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/nornir_jackedin-1.2.0-py3-none-any.whl
```

The packages are not on PyPI yet. See `JackedIN-Python-Guide.md` and the Python section of the user's guide.

## Known issues

- On Linux, JackedIN may crash when a screen reader (AT-SPI) is running; it is fine when no screen reader is active. A fix is planned.
- On Linux, screen readers may not announce terminal output yet. A fix is planned.
- On Linux, the screen reader may take a second or two to announce the Sign-in box. A fix is planned.
- Python: with JackedIN 1.2.0, leave `username` unset on a console that only asks for `Password:`. If a library call says `JackedIN did not return JSON.`, run `jackedin license status`; the trial may have ended. Both are planned fixes for the next update.
- The Windows installer and the portable zip are not code-signed. SmartScreen may warn on first run; choose **More info**, then **Run anyway**.

## Downloads

| File | For |
| --- | --- |
| `jackedin_1.2.0_windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, user's guide) |
| `JackedIN_1.2.0_x64-setup.exe` | Windows 10/11 x64 installer (unsigned) |
| `JackedIN_1.2.0_amd64.deb` | Ubuntu / Debian x64 |
| `jackedin_1.2.0_linux_x64.zip` | Other Linux x64 (portable binary + user's guide) |
| `JackedIN_1.2.0_arm64.deb` | Raspberry Pi OS 64-bit (arm64) |
| `jackedin_1.2.0_linux_arm64.tar.gz` | Raspberry Pi OS 64-bit, portable (binary + user's guide) |
| `jackedin_1.2.0_linux_arm64` | Raspberry Pi OS 64-bit, portable binary only |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `jackedin-1.2.0-py3-none-any.whl` | Python client (`pip install` the release URL) |
| `nornir_jackedin-1.2.0-py3-none-any.whl` | Nornir plugin (install after `jackedin`) |
| `JackedIN-Python-Guide.md` | Python guide: install, dry-run, expect rules, Junos commit, enable mode, Nornir, pytest |
| `jackedin-python-examples-1.2.0.zip` | Notebook, Python recipe, and CI and credential recipes |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
