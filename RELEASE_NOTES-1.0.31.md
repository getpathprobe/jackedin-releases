JackedIN™ 1.0.31 — first public release for Windows and Linux.

- SSH, Telnet and serial terminal with a desktop window, a full command line (`jackedin`) and a local automation API
- **Full-featured 3-day free trial:** try it before you buy it. No account or key needed to start.
- **Buy** (trial banner, Enter license, or the expired-trial screen) opens https://getpathprobe.com/jackedin/ in your default browser; the app stays open and usable.
- Offline license key; one purchase includes 1 year of updates ($15 to renew).

Fixes in this build:
- Tool dialogs (Ping, Traceroute, Port scan): clicking into Host and typing replaces the text, and each tool remembers its own host.
- Launching JackedIN again while it is running focuses the existing window instead of starting a second copy (Windows and Linux).
- Local API: `POST /v1/sessions/wait` returns immediately when the text has already arrived; the API token persists across restarts.
- EULA and user's guide refreshed; the saved EULA.txt is rewritten on launch.

Downloads: Windows installer (`JackedIN_1.0.31_x64-setup.exe`), Windows portable (`JackedIN_1.0.31_Windows.zip`), Debian/Ubuntu (`JackedIN_1.0.31_amd64.deb`). Check them against `SHA256SUMS`.

The Windows installer is not code-signed yet; if SmartScreen warns, choose More info → Run anyway. A Mac version is coming soon.
