# JackedIN™ 1.2.2 — What's new

JackedIN 1.2.2 is a terminal for SSH, Telnet, and serial consoles on Windows 10/11, Linux, and Raspberry Pi OS (64-bit). There is no macOS build yet. Trial and license terms are unchanged: a 72-hour trial, then one license is one computer, non-transferable, with one year of updates. The SSH, Telnet, and serial code is unchanged from the release candidate that was tested on real Cisco IOS and Juniper Junos switches. This build passed a live license check, and that test license was then revoked.

**Windows:** a portable zip (`jackedin.exe`, `jackedin.com`, and `WebView2Loader.dll`) and a setup installer (`JackedIN_1.2.2_x64-setup.exe`). The `jackedin.exe` in the zip is the same file the installer writes. The installer is not code-signed, so SmartScreen may say “Windows protected your PC”. Choose **More info**, then **Run anyway**. Windows needs the WebView2 runtime.

**Raspberry Pi:** a `.deb`, a portable tarball, and the portable binary on its own, for Raspberry Pi OS 64-bit (arm64).

## What's new in 1.2.2

### AI agents: read-only by default
- MCP and the local API stay read-only. `show`, `display`, `get`, `ping`, and `traceroute` run. A command that would change the device waits until a person approves it in the window or, for `jackedin headless`, on the terminal (type `allow` or `deny`). A denial, or 60 seconds with no answer, means it is not sent. An agent cannot approve it. Pro feature, included with the trial and with a license.
- Headless approval fix: after a prompt times out, the next `allow` is accepted and the next `deny` is refused, on Windows and Linux.
- The approval dialog closes when the 60-second wait ends.
- The local API honors `hostKeyPolicy: accept-new`. A changed host key is still refused.

### plink mode
- `jackedin plink` accepts the common PuTTY plink flags. Each line from `-m`, stdin, or the trailing command waits for the device prompt. `-batch` still refuses a changed host key. `-m` does not also read stdin, and a UTF-8 BOM is not sent as a command. Pro feature, included with the trial and with a license.

### Licensing and trial
- A licensed copy checks with the activation service at startup. A revoked key stays revoked on the next launch.
- Offline, the last confirmation is honored for 24 hours. After that JackedIN says “This license has to be checked online once.”
- A trial that has been offline for more than 24 hours and never checked in says “This trial has to be checked online once.”
- Deleting the trial files or the config folder, or signing in as another user on the same computer, does not start a new 72-hour trial.

### Other
- The WebView2 cache follows `LOCALAPPDATA` when that variable is set.
- `SHA256SUMS` also lists `jackedin.exe` and `jackedin.com`, which are attached on their own.

## Python

PyPI stays at 1.2.0. This release does not include new wheels.

```sh
pip install jackedin
pip install nornir-jackedin
```

The 1.2.0 wheels remain on the [1.2.0 release](https://github.com/getpathprobe/jackedin-releases/releases/tag/v1.2.0).

## Known issues

- On Linux, JackedIN may crash when a screen reader (AT-SPI) is running; it is fine when no screen reader is active. A fix is planned.
- On Linux, screen readers may not announce terminal output yet. A fix is planned.
- The Windows installer and the portable zip are not code-signed. SmartScreen may warn on first run; choose **More info**, then **Run anyway**.
- With the PyPI packages, which are still 1.2.0, a library call can still say `JackedIN did not return JSON.` when the trial has ended. Run `jackedin license status`.

## Downloads

| File | For |
| --- | --- |
| `jackedin_1.2.2_windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, `WebView2Loader.dll`, user's guide) |
| `JackedIN_1.2.2_x64-setup.exe` | Windows 10/11 x64 installer (unsigned) |
| `JackedIN_1.2.2_amd64.deb` | Ubuntu / Debian x64 |
| `jackedin_1.2.2_linux_x64.zip` | Other Linux x64 (portable binary + user's guide) |
| `JackedIN_1.2.2_arm64.deb` | Raspberry Pi OS 64-bit (arm64) |
| `jackedin_1.2.2_linux_arm64.tar.gz` | Raspberry Pi OS 64-bit, portable (binary + user's guide) |
| `jackedin_1.2.2_linux_arm64` | Raspberry Pi OS 64-bit, portable binary only |
| `jackedin.exe`, `jackedin.com` | The Windows executables from the zip, for checksum checks |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
