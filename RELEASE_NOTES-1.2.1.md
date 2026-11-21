# JackedIN™ 1.2.1 — What's new

JackedIN 1.2.1 is a terminal for SSH, Telnet, and serial consoles on Windows 10/11, Linux, and Raspberry Pi OS (64-bit). There is no macOS build yet. Trial and license terms are unchanged: a 72-hour trial, then one license is one computer, non-transferable, with one year of updates. Tested on real Cisco IOS and Juniper Junos switches; this build passed a live license check, and that test license was then revoked.

**Windows:** a portable zip (`jackedin.exe`, `jackedin.com`, and `WebView2Loader.dll`) and a setup installer (`JackedIN_1.2.1_x64-setup.exe`). The installer is not code-signed, so SmartScreen may say “Windows protected your PC”. Choose **More info**, then **Run anyway**. Windows needs the WebView2 runtime. The portable zip includes `WebView2Loader.dll` next to `jackedin.exe`.

**Raspberry Pi:** a `.deb`, a portable tarball, and the portable binary on its own, for Raspberry Pi OS 64-bit (arm64).

## What's new in 1.2.1

- A serial console that only shows `Password:` is answered even when `--user` is set.
- The `Password:` prompt after `enable` is the enable secret, not a logout. Later commands still run. A real logout (a return to `login:`, `Username:`, or `Password:` after a command) still stops the list. Commands that were not sent are not reported as success, and expect checks are scored against output already captured. They are not sent again.
- The Windows portable zip ships `WebView2Loader.dll` beside `jackedin.exe`.

## Python

PyPI stays at 1.2.0. This release does not include new wheels.

```sh
pip install jackedin
pip install nornir-jackedin
```

The 1.2.0 wheels remain on the [1.2.0 release](https://github.com/getpathprobe/jackedin-releases/releases/tag/v1.2.0):

```sh
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/jackedin-1.2.0-py3-none-any.whl
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/nornir_jackedin-1.2.0-py3-none-any.whl
```

`nornir-jackedin` 1.2.0 depends on `jackedin` from PyPI (`jackedin>=1.2.0`).

## Known issues

- On Linux, JackedIN may crash when a screen reader (AT-SPI) is running; it is fine when no screen reader is active. A fix is planned.
- On Linux, screen readers may not announce terminal output yet. A fix is planned.
- On Linux, the screen reader may take a second or two to announce the Sign-in box. A fix is planned.
- The Windows installer and the portable zip are not code-signed. SmartScreen may warn on first run; choose **More info**, then **Run anyway**.
- With the PyPI packages, which are still 1.2.0, a library call can still say `JackedIN did not return JSON.` when the trial has ended. Run `jackedin license status`.

## Downloads

| File | For |
| --- | --- |
| `jackedin_1.2.1_windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, `WebView2Loader.dll`, user's guide) |
| `JackedIN_1.2.1_x64-setup.exe` | Windows 10/11 x64 installer (unsigned) |
| `JackedIN_1.2.1_amd64.deb` | Ubuntu / Debian x64 |
| `jackedin_1.2.1_linux_x64.zip` | Other Linux x64 (portable binary + user's guide) |
| `JackedIN_1.2.1_arm64.deb` | Raspberry Pi OS 64-bit (arm64) |
| `jackedin_1.2.1_linux_arm64.tar.gz` | Raspberry Pi OS 64-bit, portable (binary + user's guide) |
| `jackedin_1.2.1_linux_arm64` | Raspberry Pi OS 64-bit, portable binary only |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
