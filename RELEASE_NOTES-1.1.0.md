# JackedIN™ 1.1.0 — What's new

JackedIN 1.1.0 is a terminal for SSH, Telnet, and serial consoles, with a desktop window, a command line, and a local API, for Windows 10/11 and Linux. The 3-day (72-hour) trial, the license terms, and the Buy page are unchanged: one license is one computer, non-transferable, with one year of updates. A version released in that year keeps working with that key.

Tested on real Juniper hardware: this build passed a live license check and command-line and GUI testing.

**Windows:** 1.1.0 ships as the Windows portable zip. Unzip it and run `jackedin.exe` (scripts use `jackedin.com`). There is no 1.1.0 installer; the [1.0.33 installer](https://github.com/getpathprobe/jackedin-releases/releases/tag/v1.0.33) is still available.

## In the window

- **Paste:** a multi-line paste sends one line ending per pasted line, so Junos no longer shows an extra blank prompt.
- **Window title:** shows the version, for example "JackedIN 1.1.0", and the connected host and port, for example "JackedIN 1.1.0 — 192.168.50.7:22".
- **Quick connect** accepts `user@host`. The user name is filled in for you.

## Run commands on many devices: `jackedin fleet`

`jackedin fleet --inventory FILE --cmd CMD` runs a command on every device in a CSV or simple YAML inventory (host, port, protocol, profile, credential, user), with `--concurrency N` and `--output json`. A user column, or a global `--user`, is sent to each device. The credential column is a name, not a password: set `JACKEDIN_CRED_<NAME>` in the environment. Passwords are not put on child process command lines. Each failed device prints the reason (for example no route, timed out, or authentication failed).

## Config backup and diff

`jackedin backup --host H --file FILE [--dir DIR]` stores a timestamped copy of a configuration (millisecond timestamps, so backups taken in the same second do not overwrite each other). `jackedin diff LEFT RIGHT` prints a unified diff.

## Structured output

`--output json` (the same as `--json`) returns a structured result. `--template FILE` parses command output with a TextFSM-style template from a directory you supply. Without `--output json`, the parsed rows print as a table. JackedIN does not bundle a third-party template pack.

## Consoles, console servers, and serial

- `--console-user` and `--console-password` log in to a console server before the device.
- `--baud-autosense` tries 9600, 19200, 38400, 57600, and 115200. It is off unless set.
- `--wake` sends CR and break with backoff when a console stays quiet.

## AAA logins and audit

- AAA prompt handling: `--otp-timeout SEC` waits for a Duo, RSA, or one-time-code prompt.
- `--local-user` is the fallback account when the AAA server is unreachable.
- `--max-attempts` caps login retries.
- Wrong-password messages name the user and say that authentication failed.
- `--audit FILE` writes a local JSON line for each command: who, what, when, device, and result. Passwords and one-time codes are not written there.

## Vendor device profiles

Built-in profiles for Junos, Cisco IOS/NX-OS, Arista, Nokia, MikroTik and more. `--vendor` overrides banner and prompt detection.

## Licensing

Unchanged from 1.0.33. One license activates online once, through `https://jackedin-activation.getpathprobe.workers.dev`, and is then locked to that computer. A second computer is refused and needs its own license. After activation, the copy works offline; the first activation still needs to reach the service. When the 72-hour trial ends, every device command is blocked until this computer is activated.

## Known issue

- Send Break over Telnet can print one stray replacement character (�) before the next prompt. The break is sent and the session continues normally.

## Downloads

| File | For |
| --- | --- |
| `JackedIN_1.1.0_Windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, user's guide) |
| `JackedIN_1.1.0_amd64.deb` | Ubuntu / Debian x64 |
| `JackedIN_1.1.0_Linux_x64.zip` | Other Linux x64 (portable binary + user's guide) |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
