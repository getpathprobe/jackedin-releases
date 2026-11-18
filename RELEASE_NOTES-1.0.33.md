# JackedIN™ 1.0.33 — What's new

JackedIN 1.0.33 is a terminal for SSH, Telnet, and serial consoles, with a desktop window, a command line, and a local API, for Windows 10/11 and Linux. The 3-day (72-hour) trial, the license terms, and the Buy page are unchanged: one license is one computer, non-transferable, with one year of updates. A version released in that year keeps working with that key.

This build passed a live license check and command-line and GUI testing on real Juniper hardware. The Windows installer is not code-signed yet, so SmartScreen may say "Windows protected your PC" — choose More info, then Run anyway.

## Verified exec

`jackedin exec` (and the matching local API and MCP `exec` tools) runs commands on a persistent interactive session, waits for the device prompt, pages through `--More--` style pagers, and returns a structured result. Piping into `jackedin connect` is still available, but it is not the way to confirm that a change landed.

## Send Break and keepalive

Send Break from the session menu, Ctrl+Break, the tab menu, `jackedin break`, or the API/MCP `send_break` tool. Serial sends a BREAK (250–5000 ms, default 300). Telnet sends IAC BRK. SSH sends an RFC 4335 break request.

Keepalive is off by default and can be set per session or as a default (10–600 seconds). SSH sends `SSH_MSG_IGNORE`. Telnet sends IAC NOP. Optional CLI keepalive bytes are not sent during exec, typing, pagers, or confirmation prompts, and they are left out of the auto-log.

## SSH and plink-style connection handling

- Host-key pinning, with `--hostkey` and `--hostkey-policy strict|accept-new|ask`. A changed key is refused. Non-interactive runs do not wait on a prompt and do not accept a changed key.
- `--trust-host-key` and `--accept-new` accept a **new** host key only.
- Auth diagnostics name the methods the server offered and the ones that were tried, including a missing agent. `-i` loads OpenSSH and `.ppk` keys. `JACKEDIN_KEY_PASSPHRASE` can supply a key passphrase. `--auth-methods` sets the order.
- `--pty auto|force|none`. Verified exec uses a PTY. `auto` also requests one for `sudo`, `su`, and `enable`.
- `--connect-timeout`, `--retries`, `-P`, and `host:port`. DNS, refused, timeout, and unreachable are reported as separate errors. `jackedin check host:port` tests reachability.
- Known hosts live in a file. `--known-hosts` and `JACKEDIN_KNOWN_HOSTS` choose the path so a service account is not tied to one user's store. `~/.ssh/known_hosts` is still read. `--import-putty` can read PuTTY's registry key; JackedIN does not store host keys there.

## Line and character pacing, and paced paste

Verified exec waits for the prompt before the next command. `--line-delay`, `--char-delay`, and `--wait-for-echo` pace exec, piped `connect`, paste, and the API. Serial defaults to a 100 ms line delay and waits for the prompt between stdin lines. `!sleep MS` waits without sending. A paste of 20 lines or more asks for confirmation before it is sent; the lines then go out one at a time.

## Serial port listing

On launch, JackedIN lists COM and tty ports and preselects an external USB-serial adapter (FTDI, Prolific, CH340, or CP210x) when the operating system reports one as present. If none of those is listed, it uses the last port that is still present, otherwise the first port. Ports the enumerator does not report as present are omitted. `jackedin ports` prints the same names, with the USB product name when the OS provides it. `jackedin ports --all` can add Windows COM names that are still in the SERIALCOMM map and marks them as not present or PnP status unknown. This is a listing of what the OS reports, not a guarantee that every adapter or every mapped COM name will appear.

## Vendor device profiles

Built-in profiles for Junos, Cisco IOS/NX-OS, Arista, Nokia, MikroTik and more. Profiles are included for Junos, Cisco IOS / IOS-XE / NX-OS / IOS-XR / ASA, Nokia SR OS and SR Linux, Arista, HPE/Aruba ProCurve, AOS-CX, and Comware, Huawei VRP, MikroTik, FortiOS, PAN-OS, Extreme EXOS/VOSS, EdgeOS/VyOS, Dell OS10, Ciena, Calix AXOS, and Linux/BSD. `--vendor` overrides banner and prompt detection. Each profile has a prompt pattern, pager handling, a paging-off command, and error strings.

## Windows scripts: `jackedin.com`

`jackedin.exe` remains the GUI program (double-click or the Start menu opens the window, with no console). `jackedin.com` is a console program, included in the installer and in the new Windows portable zip, so `cmd` can run `jackedin exec ... > out.txt` and pipe to `findstr`. Point scripts at `jackedin.com`, not `jackedin.exe`.

## Licensing: one device, then offline use

One license activates online once, through `https://jackedin-activation.getpathprobe.workers.dev`, and is then locked to that computer. Activating again on the same computer is allowed. A second computer is refused and needs its own license. There is no deactivate or transfer.

After a successful activation, later launches check the saved activation locally. There is no periodic check-in. Exec, connect, and the window keep working if the activation service is unreachable. That is offline use **after** activation. The first activation still needs to reach the service; this is not air-gapped activation. If the first activation cannot reach the service, it fails and the copy stays unactivated.

A stored key that has not been activated on this computer says so, and tells you to run `jackedin license activate`. A key and activation file copied from another computer say that the activation belongs to a different computer. During a trial, those copies still run only as a trial, never as Licensed. When the 72-hour trial ends, every device command is blocked until this computer is activated.

## Known issues (planned for 1.1)

- A paced multi-line paste can send a double line ending, which shows up as an extra blank prompt on Junos. The commands still run in order.
- The window title shows "JackedIN" without the version number. `jackedin --version` (from the console program) prints 1.0.33.

## Downloads

| File | For |
| --- | --- |
| `JackedIN_1.0.33_x64-setup.exe` | Windows 10/11 x64 installer (per-user, no admin needed; not code-signed yet) |
| `JackedIN_1.0.33_Windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, user's guide) |
| `JackedIN_1.0.33_amd64.deb` | Ubuntu / Debian x64 |
| `JackedIN_1.0.33_Linux_x64.zip` | Other Linux x64 (portable binary + user's guide) |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
