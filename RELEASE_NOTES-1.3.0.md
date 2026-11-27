# JackedIN™ 1.3.0 — What's new

JackedIN 1.3.0 is a terminal for SSH, Telnet, and serial consoles on Windows 10/11, Linux, and Raspberry Pi OS (64-bit). There is no macOS build yet. Trial and license terms are unchanged: a 72-hour trial, then one license is one computer, non-transferable, with one year of updates. This build passed a live license check, and that test license was then revoked.

**Windows:** a portable zip (`jackedin.exe`, `jackedin.com`, `WebView2Loader.dll`, and `jackedin.integrity`) and a setup installer (`JackedIN_1.3.0_x64-setup.exe`). The `jackedin.exe` in the zip is the same file the installer writes. The installer is not code-signed, so SmartScreen may say “Windows protected your PC”. Choose **More info**, then **Run anyway**. Windows needs the WebView2 runtime.

**Linux and Raspberry Pi:** a `.deb` for each, the standalone binary with its `.integrity` file, and a portable bundle (`jackedin_1.3.0_linux_x64.zip`, `jackedin_1.3.0_linux_arm64.tar.gz`) with `jackedin`, `jackedin-cli`, `jackedin.integrity`, the user's guide, examples, and shell completions.

## What's new in 1.3.0

### Batch mode: `jackedin fleet`
- Run one command, or a whole command file, across many devices in one go: `jackedin fleet --inventory devices.csv --file commands.txt`.
- Works over **SSH, Telnet, and serial consoles**, chosen per device by the inventory's `protocol` column. Mixed inventories are fine.
- Each device waits for its prompt (or `--terminator`) and pages through `--More--`, so long `show` output arrives complete. `--timeout` is per device, `--pace` adds a delay after each prompt, and `--concurrency` sets how many devices run at once. `--dry-run` prints the plan and connects to nothing.
- Credentials are names, not passwords: set `JACKEDIN_CRED_<NAME>`, or use the OS keychain or the credentials vault. An `enable_env` column supplies a Cisco enable secret from an environment variable.

### JSON, CSV, and text output
- `--output json|csv|text`. In JSON, each device's `output` is the per-command report (command, ok, prompt, timed_out, duration, output), and `text` is the command outputs joined. The enable `Password:` prompt is left out of both.

### Exit codes for scripts
- `0` every device complete, `1` a login or command failure, `3` a timeout or partial output with nothing worse, `2` bad usage. A connection that drops after printing something is `partial` and exit 3. See `docs/examples/EXIT-CODES.md`.

### Reliable Cisco console recovery after timeouts
- When a serial command times out, JackedIN sends the IOS break sequence, drains the line until it goes quiet, and exits 3.
- The next run on that console clears any leftover output first, waits for a clean prompt, and only then sends `terminal length 0`. Output from the interrupted command no longer spills into the next run, in user mode or enable mode.

### Ansible
- The bundled `jackedin.terminal` collection's `jackedin_fleet` module passes the new fleet options through.

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
| `jackedin_1.3.0_windows_x64.zip` | Windows 10/11 x64 portable (`jackedin.exe`, `jackedin.com`, `WebView2Loader.dll`, `jackedin.integrity`, user's guide) |
| `JackedIN_1.3.0_x64-setup.exe` | Windows 10/11 x64 installer (unsigned) |
| `JackedIN_1.3.0_amd64.deb` | Ubuntu / Debian x64 |
| `jackedin_1.3.0_linux_x64` + `jackedin_1.3.0_linux_x64.integrity` | Other Linux x64, standalone binary (keep both files together) |
| `jackedin_1.3.0_linux_x64.zip` | Other Linux x64, portable bundle (`jackedin`, `jackedin-cli`, `jackedin.integrity`, guide, examples) |
| `JackedIN_1.3.0_arm64.deb` | Raspberry Pi OS 64-bit (arm64) |
| `jackedin_1.3.0_linux_arm64` + `jackedin_1.3.0_linux_arm64.integrity` | Raspberry Pi OS 64-bit, standalone binary (keep both files together) |
| `jackedin_1.3.0_linux_arm64.tar.gz` | Raspberry Pi OS 64-bit, portable bundle |
| `jackedin.exe`, `jackedin.com`, `jackedin.integrity` | The Windows programs and manifest from the zip, for checksum checks |
| `EULA.txt`, `JackedIN-Users-Guide.html`, `JackedIN-Users-Guide.md` | License agreement and user's guide |
| `SHA256SUMS` | Checksums |

Buy and trial: https://getjackedin.com (forwards to https://getpathprobe.com/jackedin/).
