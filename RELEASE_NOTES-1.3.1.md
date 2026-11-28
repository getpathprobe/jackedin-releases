# JackedIN™ 1.3.1 — What's new

JackedIN 1.3.1 is a small fix release for Windows 10/11, Linux x86_64 (Debian/Ubuntu), and Raspberry Pi OS 64-bit (arm64). Trial and license terms are unchanged: a 72-hour trial, then one license is one computer, non-transferable, with one year of updates. This build passed a live license check (online activation, second-computer refusal, fresh 72-hour trial, tamper refusal), and the test licenses were then revoked.

## What's new in 1.3.1
- `jackedin license status` now shows the date this build was made on the `this release:` line. 1.3.0 always showed 2026-11-10. Licensing and update-eligibility checks are unchanged.

## Downloads
- **Windows:** portable zip (`jackedin_1.3.1_windows_x64.zip`) and the setup installer (`JackedIN_1.3.1_x64-setup.exe`). The installer is not code-signed, so SmartScreen may say "Windows protected your PC". Choose **More info**, then **Run anyway**.
- **Linux x86_64:** `JackedIN_1.3.1_amd64.deb`, the standalone `jackedin_1.3.1_linux_x64` with its `.integrity` file (keep both together), or the portable bundle `jackedin_1.3.1_linux_amd64.tar.gz`.
- **Raspberry Pi OS 64-bit (arm64):** `JackedIN_1.3.1_arm64.deb` or the portable bundle `jackedin_1.3.1_linux_arm64.tar.gz`. The arm64 build was added after the x86 files and passed the same live license check on a Raspberry Pi.

Every program checks itself against its signed `.integrity` manifest, so a modified copy is refused. Verify downloads with `SHA256SUMS`.
