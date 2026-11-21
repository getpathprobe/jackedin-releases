# JackedIN™ — release downloads

JackedIN™ is an SSH, Telnet and serial terminal for network engineers, with a desktop window (GUI), a full command line (CLI) and a local automation API, for Windows, Linux and Raspberry Pi OS (64-bit). There is no macOS build yet.

This repository contains **release binaries and documentation only**. Source code is not published here.

**Try it before you buy it:** every download includes a full-featured 3-day free trial. After the trial, a license key is required. Buy at https://getpathprobe.com/jackedin/ — $19 launch price (regular $29), one-time, with 1 year of updates. **One license = one computer, non-transferable:** the key activates online once and is then locked to that computer.

Support: service@getpathprobe.com

## Download

Get the latest version from the [Releases page](https://github.com/getpathprobe/jackedin-releases/releases/latest).

| Platform | File |
|---|---|
| Windows 10/11 x64 portable | `jackedin_1.2.0_windows_x64.zip` |
| Windows 10/11 x64 installer | `JackedIN_1.2.0_x64-setup.exe` |
| Debian/Ubuntu x86_64 | `JackedIN_1.2.0_amd64.deb` |
| Linux x86_64 portable | `jackedin_1.2.0_linux_x64.zip` |
| Raspberry Pi OS 64-bit (arm64) | `JackedIN_1.2.0_arm64.deb` |
| Raspberry Pi OS 64-bit portable | `jackedin_1.2.0_linux_arm64.tar.gz` |
| Raspberry Pi OS 64-bit portable binary only | `jackedin_1.2.0_linux_arm64` |
| Python client / Nornir plugin (any OS) | `jackedin-1.2.0-py3-none-any.whl`, `nornir_jackedin-1.2.0-py3-none-any.whl` |

Verify downloads with `SHA256SUMS`.

## Install

**Windows:** unzip `jackedin_1.2.0_windows_x64.zip` and run `jackedin.exe` (scripts use `jackedin.com`). No admin rights are needed. An installer is also available: `JackedIN_1.2.0_x64-setup.exe`. It is not code-signed, so SmartScreen may say "Windows protected your PC": choose **More info**, then **Run anyway**.

**Ubuntu / Debian:**
```sh
sudo apt install ./JackedIN_1.2.0_amd64.deb
jackedin --version
```

**Raspberry Pi OS 64-bit:**
```sh
sudo apt install ./JackedIN_1.2.0_arm64.deb
jackedin --version
```

## Python

The `jackedin` Python client and the `nornir-jackedin` Nornir plugin are attached to the 1.2.0 release. They are free and drive the installed JackedIN app (72-hour trial, then a license):

```sh
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/jackedin-1.2.0-py3-none-any.whl
pip install https://github.com/getpathprobe/jackedin-releases/releases/download/v1.2.0/nornir_jackedin-1.2.0-py3-none-any.whl
```

See `JackedIN-Python-Guide.md`. Examples and CI recipes are in `jackedin-python-examples-1.2.0.zip`.

## License

Proprietary. Use is governed by the End User License Agreement in `EULA.txt`. JackedIN™ is an unregistered trademark. All sales are final, no refunds except where required by law. Our order process is conducted by our online reseller Paddle.com, the Merchant of Record for all our orders.
