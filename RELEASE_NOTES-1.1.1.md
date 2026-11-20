# JackedIN™ 1.1.1 — What's new

JackedIN 1.1.1 is a terminal for SSH, Telnet, and serial consoles on Windows 10/11, Linux, and Raspberry Pi OS (64-bit). Trial and license terms are unchanged: one license is one computer, non-transferable, with one year of updates. Tested on real Cisco IOS and Juniper Junos switches; each build passed a live license check.

**Windows:** a portable zip (`jackedin.exe`; scripts use `jackedin.com`). There is no 1.1.1 installer; the [1.0.33 installer](https://github.com/getpathprobe/jackedin-releases/releases/tag/v1.0.33) is still available.

**Raspberry Pi:** new in 1.1.1, for Raspberry Pi OS 64-bit (arm64): a `.deb`, a portable zip, and the portable binary on its own.

## What's new

- Older SSH devices can connect. A notice names any legacy algorithms in use; `--no-legacy-ssh` turns them off.
- First-connect host-key dialog with **Trust and connect**, **Connect once**, and **Cancel**. A changed host key is refused with a warning, and `--trust-host-key` never accepts a changed key.
- Cancel on sign-in does not send a password.
- Sign-in takes the password right away, even after the host-key dialog was left open for a while (on Windows, keystrokes could be lost).
- The “who else is logged in” check is off until you turn it on.
- A silent or missing serial port explains the problem and suggests baud rate, autosense, wake, or `jackedin ports`.
- Session logs drop extra carriage returns, NULs, and escape sequences (`--raw` keeps them). The app log records connect and disconnect, with no passwords.
- A correct console password still works after a wrong one. A leftover “Login incorrect” is not treated as a new failure.
- Device profiles for Junos, Cisco IOS and NX-OS, Nokia, and many more (`--vendor`); only Cisco IOS and Junos were tested on real hardware.
- F11 toggles full screen and returns to the normal window without losing focus. Closing full screen no longer saves that size on Linux.
- Quick connect uses the selected protocol. Reconnect reuses the tab. The `e` key selects Serial and clears the port. Switching protocols resets the port.
- Large output no longer freezes the terminal.

## Known issues

- On Linux, JackedIN may crash when a screen reader (AT-SPI) is running; it is fine when no screen reader is active. A fix is planned.
- On Linux, screen readers may not announce terminal output yet. A fix is planned.
- On Linux, the screen reader may take a second or two to announce the Sign-in box. A fix is planned.

## Downloads

| File | For |
| --- | --- |
| `JackedIN_1.1.1_Windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, user's guide) |
| `JackedIN_1.1.1_amd64.deb` | Ubuntu / Debian x64 |
| `JackedIN_1.1.1_Linux_x64.zip` | Other Linux x64 (portable binary + user's guide) |
| `JackedIN_1.1.1_arm64.deb` | Raspberry Pi OS 64-bit (arm64) |
| `JackedIN_1.1.1_Linux_arm64.zip` | Raspberry Pi OS 64-bit, portable (binary + user's guide) |
| `jackedin_1.1.1_linux_arm64` | Raspberry Pi OS 64-bit, portable binary only |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
