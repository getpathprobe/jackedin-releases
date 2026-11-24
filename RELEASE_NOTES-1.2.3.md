# JackedIN™ 1.2.3 — What's new

JackedIN 1.2.3 is a terminal for SSH, Telnet, and serial consoles on Windows 10/11, Linux, and Raspberry Pi OS (64-bit). There is no macOS build yet. Trial and license terms are unchanged: a 72-hour trial, then one license is one computer, non-transferable, with one year of updates. The SSH, Telnet, serial, plink, and AI-approval code is unchanged from 1.2.2. This build passed a live license check, and that test license was then revoked.

**Windows:** a portable zip (`jackedin.exe`, `jackedin.com`, `WebView2Loader.dll`, and `jackedin.integrity`) and a setup installer (`JackedIN_1.2.3_x64-setup.exe`). The `jackedin.exe` in the zip is the same file the installer writes. The installer is not code-signed, so SmartScreen may say “Windows protected your PC”. Choose **More info**, then **Run anyway**. Windows needs the WebView2 runtime.

**Linux and Raspberry Pi:** a `.deb` for each, and the standalone binary with its `.integrity` file.

## What's new in 1.2.3

### Integrity check
- Every shipped program checks itself against a signed manifest at startup. This covers `jackedin.exe` and `jackedin.com` on Windows, and `jackedin` and `jackedin-cli` on Linux.
- A modified or damaged copy is refused with: “This copy is damaged or has been modified; re-download from getpathprobe.com.” It stays on the trial and does not touch your license files.
- **No change for paying customers.** An existing license keeps working after the update, online and offline, with no extra step.
- The zip and the installer ship `jackedin.integrity` next to the programs. The `.deb` puts it in `/usr/bin`.
- **Standalone Linux binaries** (`jackedin_1.2.3_linux_x64`, `jackedin_1.2.3_linux_arm64`) come with a `<name>.integrity` file. Download both and keep them side by side in the same folder. If you rename the binary, rename its `.integrity` file to match, or rename them to `jackedin` and `jackedin.integrity`.

### Downloads
- The Linux x64 portable zip and the Raspberry Pi portable tarball are replaced by the standalone binary plus its `.integrity` file.
- `SHA256SUMS` lists every file, including the `.integrity` files.

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
| `jackedin_1.2.3_windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, `WebView2Loader.dll`, `jackedin.integrity`, user's guide) |
| `JackedIN_1.2.3_x64-setup.exe` | Windows 10/11 x64 installer (unsigned) |
| `JackedIN_1.2.3_amd64.deb` | Ubuntu / Debian x64 |
| `jackedin_1.2.3_linux_x64` + `jackedin_1.2.3_linux_x64.integrity` | Other Linux x64, standalone binary (keep both files together) |
| `JackedIN_1.2.3_arm64.deb` | Raspberry Pi OS 64-bit (arm64) |
| `jackedin_1.2.3_linux_arm64` + `jackedin_1.2.3_linux_arm64.integrity` | Raspberry Pi OS 64-bit, standalone binary (keep both files together) |
| `jackedin.exe`, `jackedin.com`, `jackedin.integrity` | The Windows programs and manifest from the zip, for checksum checks |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
