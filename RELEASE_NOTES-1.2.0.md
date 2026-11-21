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

## Known issues

- On Linux, JackedIN may crash when a screen reader (AT-SPI) is running; it is fine when no screen reader is active. A fix is planned.
- On Linux, screen readers may not announce terminal output yet. A fix is planned.
- On Linux, the screen reader may take a second or two to announce the Sign-in box. A fix is planned.
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
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
