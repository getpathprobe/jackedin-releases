# JackedIN™ User's Guide

Copyright © 2026 JackedIN. All rights reserved.

JackedIN™ is an SSH, Telnet, and serial terminal. It has a desktop window and a full command line. This guide covers both, on Windows and on Linux. A macOS build is coming soon. JackedIN™ is an unregistered trademark. The software is offered under the proprietary end-user license in `LICENSE/EULA.txt`, not under an open-source license.

The command is `jackedin`. With no arguments it opens the window. With a command it stays in the terminal, prints a result or an error, and exits. An unknown command or flag prints usage and exits with status 2. It does not open the window.

SFTP file transfer is not included.

## Install

### Windows

Run `JackedIN_1.0.28_x64-setup.exe` and follow the installer. The Start menu entry is JackedIN. The command is added for the current user when the installer finishes. `jackedin --version` prints `1.0.28`.

Windows SmartScreen may say “Windows protected your PC” because the installer is not signed. Choose **More info**, then **Run anyway**.

The installer shows the end-user license and asks you to accept it before it copies files. The first time the window opens, on Windows or Linux, JackedIN shows the same license again. Choose **I accept** to continue. **I do not accept** exits JackedIN and does not record acceptance. Acceptance is stored in settings.

The portable zip is the same program without an installer. Unzip it and run `jackedin.exe`. The user's guide files sit next to the executable.

### Linux

Install the Ubuntu package:

```bash
sudo apt install ./JackedIN_1.0.28_amd64.deb
```

The package depends on WebKitGTK 4.1, GTK 3, Ayatana AppIndicator, iputils-ping, and traceroute (or iputils-tracepath). The command is `jackedin`. The user's guide is installed with the package resources (this file and the HTML copy).

### macOS

A macOS build is coming soon. This guide does not describe a current macOS installer.

## Paid license

JackedIN™ is a paid download. A purchase includes the app and one year of updates. A $15 renewal extends that year. One purchase is a single-user license. You may not redistribute, resell, or share the license key. Help → About, and Settings → About, show the email, order id, and updates-until date from the key that unlocked this copy. During the trial, About shows Trial instead of an email.

The license is an offline key signed by the seller. It names the buyer email, the order id, the product JackedIN, the issue date, and the updates-until date (the purchase date plus one year). The app checks the signature with a public key built into the program. The private key is not in the app.

A version released on or before updates-until keeps working forever. A version released after that date still starts, and it shows **updates expired, renew** until you activate a renewal key. It does not pretend the old key covers the new build.

### Activate in the window

After the trial ends, until a valid key is stored, the window is the activation screen and the command line and local API refuse to open a session or run a tool. The window says **Trial expired, buy a license**. Buy JackedIN at https://jackedin.app. Paste the key from the purchase email and choose Activate, or run `jackedin license activate`. JackedIN writes it to `license.key` in the config directory and checks it every time it starts. A changed or incomplete key is rejected and not stored. A valid key ends the trial. A licensed copy does not show the trial countdown.

The end-user license is shown only the first time JackedIN runs on that computer. Acceptance is the EULA version and the time it was accepted, stored in the config folder: `%APPDATA%\JackedIN` on Windows and `~/.config/jackedin` on Linux. Later launches skip it. A new version of the agreement asks again. **I do not accept** exits without saving that record and without running. `jackedin eula accept` or `--accept-eula` on a command records the same acceptance for the command line.

### Activate from the command line

Windows and Linux use the same commands:

```bash
jackedin license activate 'PASTE-THE-KEY'
jackedin license status
```

`status` prints the email, order, updates-until date, and this build's release date. During the trial it prints the time left, for example `Trial: 2 days 5 h left, Buy / Enter license`, and exits 0. After the trial, with no key, it exits with an error and tells you to activate. `connect`, `scan`, `ping`, `trace`, and the other product commands do the same once the trial is over. `--help` and `--version` do not need a key.

Those commands also require the license agreement. `jackedin eula` prints the path of `EULA.txt` in the config folder. `jackedin eula accept` records acceptance. `--accept-eula` on a command does the same thing. `--help` and `--version` do not require it.

## Trial

The first time the agreement is accepted on a computer, JackedIN starts a 3-day trial. For 72 hours the window, the command line, and the local API all work without a license key. The window shows `Trial: 2 days 5 h left, Buy / Enter license` on a banner and in the status bar. **Buy** opens the purchase page. **Enter license** is the same Activate box used after the trial. Help → About and Settings → About show Trial. `jackedin license status` prints that countdown. The local API `GET /v1/health` response includes a `trial` field (`state`, `expiresAt`, `remainingSeconds`, `message`).

Windows stores the trial in `%APPDATA%\JackedIN` and in the registry key `HKCU\Software\JackedIN`. Linux stores it in `~/.config/jackedin` and `~/.local/share/jackedin`. Each copy is tied to that computer. Uninstalling JackedIN does not delete those markers, on Windows or on Linux, so installing again does not start a new 3 days. Removing one copy while the other remains ends the trial. Setting the clock back more than a few minutes ends it too.

When the 72 hours are up, the window, the command line, and the API lock. The message is **Trial expired, buy a license**, followed by the purchase page and `jackedin license activate`. Entering a valid key at any time ends the trial and unlocks the copy. A licensed user does not see the trial banner.

## What a license includes

Everything in the window and the command line is part of the paid app: SSH, Telnet, serial, tabs, saved sessions, logging, reconnect, ping and traceroute, the log tail, the port scanner, the session-limit test, the other-sessions count, Wireshark capture, and the local API. SFTP is not included. Items that used to be marked Pro are included with the license. They are not a separate free tier.

## First launch

The first paint is the JackedIN logo and “Opening the session list…”. That splash stays up until the session list is ready. Settings live under the gear. About is also on the Help menu. Logging is on. The log folder is `Documents/JackedIN/Logs` (Windows: your Documents folder; Linux: `~/Documents/JackedIN/Logs`).

A second launch, or clicking the JackedIN icon while it is already running, brings the existing window forward. On Linux that includes restoring a minimized window. Closing the window quits JackedIN unless Settings has minimize-to-tray turned on.

## The window

### Quick connect

The bar at the top picks SSH, Telnet, or serial, takes a host or device, and connects when you press Enter. SSH fills a blank user, port, key, and jump host from `~/.ssh/config`, then tries ssh-agent and the default keys. Ctrl+Shift+K (Command+K on a future macOS build) focuses the field.

### Tabs

Ctrl+Alt+T opens a tab. Ctrl+Tab and Ctrl+Shift+Tab move between tabs. Ctrl+Alt+1 through 9 jumps to a tab. Drag a tab out of the window to move it. Right-click a tab to duplicate it or move it to a new window. Ctrl+Shift+N opens another window. Every window shares saved sessions and settings. Panes split right (Ctrl+Alt+S) or down (Ctrl+Alt+Shift+S).

### SSH

Choose SSH, type the host and user, and connect. A password, a private key (OpenSSH or PuTTY `.ppk`), or ssh-agent can authenticate. On Linux the agent is the socket in `SSH_AUTH_SOCK`. On Windows, Pageant and the Windows OpenSSH agent are used. Blank user, port, and key fields are filled from `~/.ssh/config` when the host matches, including one `ProxyJump`. Default key files are `~/.ssh/id_ed25519`, `id_ecdsa`, and `id_rsa`.

The first time a host is seen, the dialog is titled **Trust this host key** and shows the fingerprint. Compare it with the device, then tick Trust this host key and connect again. That stores this fingerprint for this connection only. A recent connection created from the command line uses the same checkbox; it does not keep the terminal’s `--trust-host-key` wording or policy. A changed host key always warns.

A keyboard-interactive prompt (a one-time code, for example) is asked after the public key is accepted. A wrong code says the verification code was wrong. A wrong password says the server rejected that password.

### Telnet

Choose Telnet. The default port is 23. Window size and terminal type are negotiated. Use this for a switch or router management address when SSH is not available.

### Serial

On launch JackedIN lists COM and tty ports and preselects an external USB-serial adapter (FTDI, Prolific, CH340, or CP210x) when one is present. If none of those is listed, the box starts on the last port that is still present, otherwise the first port. If that last port is gone, the dialog says so. You can still type a path. `jackedin ports` prints the same names, with the USB product name when the operating system provides it.

| | Windows | Linux |
| --- | --- | --- |
| Device | `COM5` | `/dev/ttyUSB0` or `/dev/serial/by-id/...` |
| Typical console | 9600 8N1, no flow control | the same |

Install the adapter driver if Windows does not list the port. Close any other program that has the COM port open. On Linux, opening the device requires membership in the `dialout` group. Some systems use `uucp` or `lock` instead. Add your user, then log out and back in:

```bash
sudo usermod -aG dialout "$USER"
```

A permission error names the group to join and tells you to log out and back in. It does not suggest ping or traceroute. A missing COM port or `/dev` path says the port was not found and points at `jackedin ports`. Other serial errors talk about the device path and baud rate.

The status bar shows the protocol, the device, the line settings (`9600 8N1 no flow`), and whether the log is on. It does not show “via” an IP address for a serial session.

### Source interface

For SSH and Telnet, **Source interface** lists adapters that have an address. **System routing** lets the operating system pick. Each row shows the adapter name, its address, and a state such as Up, Disconnected, Virtual, or Loopback, and it marks the default route. The outgoing TCP connection is bound to the address you pick. One active interface is preselected. When several are up, the address on the default route is preselected. The list fills in after the window opens. If it is still empty when you open New connection, JackedIN asks again. Serial does not use a source address.

Packet capture uses a separate NIC question. When capture is on and more than one adapter is up, JackedIN asks which NIC to capture, highlights the one that routes to the host, and can remember that choice for the session. A connection to localhost captures on the loopback adapter.

### Terminal, font, and the status bar

The grid is fitted to the visible pane. Columns stop to the left of the scrollbar, and rows fill the pane height, including the small pad under the last line. Changing the window size, the sidebar, or the zoom refits the grid. The status bar shows the font size you see. At 100% zoom that is the size in Settings, 12 pt by default. Ctrl plus, Ctrl minus, and Ctrl 0 (Command on a future macOS build) zoom the window. The readout changes with the zoom. The font size stored in Settings does not. View has the same three commands. The choice is saved.

On a narrow window, lower-priority status fields hide so the protocol, the host, and the connection state stay readable. The protocol label keeps enough width that “SSH” is not cut down to “S”.

### Saved sessions

Saved sessions live in the sidebar, in folders. Click a session (or activate it with a keyboard or a screen reader) to connect. The name in the Save session box is the name that is stored. A default name follows the current tab: the host on SSH or Telnet, the serial port on Serial. Switching from Serial to SSH replaces a leftover port name such as COM5 with the host. A name you typed stays.

Each protocol keeps only its own fields. An SSH session keeps the private-key path and drops serial line settings. Telnet and serial drop the key path, the key passphrase, and the host-key policy. Serial also drops the host and the TCP port. Trust this host key stores the fingerprint for that connection. It is not saved as a permanent “accept any future key” flag. Stale fields from another protocol are removed when you save, and again when JackedIN starts.

Delete asks you to confirm before the saved session is removed. An open terminal and the log files stay. Recent connections are the last few targets. The same host and port are listed once. A recent started from the command line does not keep that command’s `--log`, `--raw`, or `--no-log` choice. Opening it in the window writes a normal log in the log folder. Remove one from the list, or clear the list, without deleting a saved session or a log file.

### Capture

“Start Wireshark capture before connecting” looks for `dumpcap` (from Wireshark or tshark) and captures on the interface that reaches the host. A `host` filter limits the file to that target. A connection to localhost uses the loopback adapter, and the filter is that session’s TCP port. Tick “Record all loopback traffic” to keep the wider capture. The status bar can open the capture file.

What has to be installed:

| | Prerequisite |
| --- | --- |
| Windows | Wireshark (for `dumpcap`) and Npcap. If Npcap was installed with “Restrict Npcap driver's access to Administrators only”, capture works only when JackedIN is run as administrator. Reinstall Npcap and leave that option unchecked to capture as a normal user. |
| Linux | Wireshark or tshark so `dumpcap` is on the path, and membership in the `wireshark` group, or `cap_net_raw` on `dumpcap`. `tcpdump` is not required. |

If something is missing, the dialog says what it is and still lets you connect without capture. The check is cached, so startup does not wait on it.

### Logging

Each session writes `YYYY-MM-DD_HHMMSS_<target>.log` in the log folder unless you clear **Log this session**. The file is readable text: a run of carriage returns followed by a line feed (including the CR CR LF a Junos console sends) becomes one newline, NUL bytes are dropped, and escape sequences are removed. The command line uses the same cleaning. The live terminal still shows the device output. Open the log with the log tail (Ctrl+Shift+O).

### When a session drops

A dropped SSH or Telnet session reopens the dialog as **Reconnect**, titled **Could not stay connected**, with the address still filled in. Ping and traceroute run only if you click them, unless Settings or the session turned that on. A serial failure uses the serial wording above. Closing a session yourself does not open the dialog.

### Other sessions

After an SSH login, JackedIN can ask who else is logged in on a separate channel. The status line stays on one line. Hover it for the longer note. The count leaves out this SSH login. It states the two counts separately, for example “1 other login on the device · 0 other JackedIN sessions to this host”. A desktop login that `who` lists twice (the seat and `:0`) counts once. When the device is not Linux, macOS, or Junos, the line stays blank rather than showing a wrong count. When nobody else is logged in and no other JackedIN session is open to that host, it reads “no other device sessions seen”.

Automatic mode uses `who` on Linux and macOS. It reads this session's pts with the shell's `tty` (not the short check command) and drops that row. A localhost login is the same session when `who` prints `localhost` and the connection is `127.0.0.1` or `::1`. Junos is not counted by `who`. Automatic asks `show version`, and on a root shell `cli -c "show version | no-more"`. If either says Junos, it uses `cli -c "show system users | no-more"`, then `show system users | no-more` if that is not the user table. Virtual-chassis lines such as `fpc0:` and the row of dashes are not users. If Automatic still shows no count, choose the Juniper profile on the connection. The console login stays. The check runs again every 60 seconds. Each pass is written to `jackedin.log` in the log folder.

Cisco IOS, NX-OS, Juniper, and Arista profiles are on the connection dialog. Linux / Unix who uses the same `who` reading as Automatic, including dropping our own pts. A custom command is there too. “Don't check” turns the count off for that session.

Tools → Ping and Tools → Traceroute each open a dialog and show the result. `jackedin ping --host H` and `jackedin trace --host H` are the same checks from the command line. Clicking a saved session that is already connected focuses that tab instead of opening another one.

### Port scan

Port scan is in the Tools menu. It is a TCP connect scan from the source address you picked. It does not need extra privileges. Presets are common admin ports, the top 100, or a list or range such as `22,80,443` or `1-1024`. The table shows the port, the state, a likely service, and an SSH or Telnet banner on ports 22 and 23. Telnet negotiation bytes are not shown in that banner. Double-click an open port to fill the host, port, and protocol in the connection dialog. The first scan shows a one-time notice: only scan devices you are allowed to test. Results are saved in the log folder. Scan, ping, and traceroute each have a Cancel button and do not block the window. `jackedin scan` is the same scan from the command line.

### Session-limit test

The session-limit test is Max-session test in the Tools menu, or Ctrl+Shift+M. It warns that many simultaneous logins can lock an account. After you confirm, it opens the number of sessions you set (up to 40) in a tile grid and reports which ones connected. When some succeed and the rest are refused or reset, the summary says the max number of users was likely reached.

### Keyboard shortcuts

Windows and Linux use Ctrl or Ctrl+Shift so that Ctrl+C still reaches the session. The in-app Shortcuts screen (F1) lists every binding. macOS bindings below are for the coming macOS build.

| Action | Windows / Linux | macOS (coming soon) |
| --- | --- | --- |
| New connection | Ctrl+Shift+T | Cmd+N |
| New tab | Ctrl+Alt+T | Cmd+T |
| New window | Ctrl+Shift+N | Cmd+Shift+N |
| Close tab | Ctrl+Shift+W | Cmd+W |
| Next / previous tab | Ctrl+Tab / Ctrl+Shift+Tab | same, plus Cmd+Shift+] / [ |
| Jump to tab 1–9 | Ctrl+Alt+1–9 | Cmd+1–9 |
| Copy / paste | Ctrl+Shift+C / V | Cmd+C / V |
| Find | Ctrl+Shift+F | Cmd+F |
| Zoom in / out / reset | Ctrl++ / Ctrl+- / Ctrl+0 | Cmd++ / Cmd+- / Cmd+0 |
| Reconnect | Ctrl+Shift+R | Cmd+Shift+R |
| Duplicate session | Ctrl+Shift+D | Cmd+Shift+D |
| Tail session log | Ctrl+Shift+O | Cmd+Shift+O |
| Toggle logging | Ctrl+Shift+L | Cmd+Shift+L |
| Settings | Ctrl+, | Cmd+, |
| Command palette | Ctrl+Shift+P | Cmd+Shift+P |
| Focus quick connect | Ctrl+Shift+K | Cmd+K |
| Split right / down | Ctrl+Alt+S / Ctrl+Alt+Shift+S | Cmd+\ / Cmd+Shift+\ |
| Toggle sidebar | Ctrl+Shift+B | Cmd+Shift+B |
| Session-limit test | Ctrl+Shift+M | Cmd+Shift+M |
| Fullscreen | F11 | Ctrl+Cmd+F |
| Shortcuts | F1 | Cmd+/ |
| Launch hotkey | Ctrl+Alt+J | Cmd+Option+J |

Right-click pastes into the terminal. Selecting text copies it. Port scan and traceroute are in the Tools menu. They have no extra shortcut so the session keeps those keys. The launch hotkey focuses quick connect while JackedIN is already running. The Windows installer also sets Ctrl+Alt+J on the Start menu entry so it can start the app when it is not running.

## The command line

`jackedin --help` and `jackedin --version` print and exit. They do not need a display. Any other argument is a command: an unknown word such as `jackedin serial --help` prints usage and exits 2.

Logging matches the window: on by default, using the log folder from Settings. The program prints `log <path>` after it connects. `--no-log` disables the file. `--log FILE` appends that file. `--raw` keeps control codes in the log and on standard output. Without `--raw`, standard output is cleaned the same way as the log file. `connect --cmd` on SSH writes that command’s output into the same log.

A pipe is sent to the session for Telnet and for an interactive SSH shell, including bytes written a few seconds after the program starts. Reading continues until the writer closes the pipe. On Windows the installed app is a windowed program: it reads the pipe cmd.exe or another program inherited (`echo ... | jackedin connect ...`), not the console keyboard.

```bash
echo 'show version' | jackedin connect --protocol telnet --host 192.0.2.10 --port 23
```

`--baud abc` is an error. The rate has to be a number from 1 to 12000000. You can omit `--protocol serial` when you pass `--serial`, `--device`, or `--baud`, or when `--host` looks like `COM5` or `/dev/ttyUSB0`. A missing port names the ports that exist and tells you to run `jackedin ports`.

### Serial console at 9600 8N1

Windows, COM5:

```bash
jackedin ports
jackedin connect --protocol serial --host COM5 --port 9600
```

Linux, `/dev/ttyUSB0`, explicit 8N1:

```bash
jackedin ports
jackedin connect --protocol serial --serial /dev/ttyUSB0 --baud 9600 --data-bits 8 --parity none --stop-bits 1 --flow none
```

`--host COM5 --port 9600` and `--serial /dev/ttyUSB0 --baud 9600` are the same kind of session, and `--protocol serial` can be left off. `--port` is the baud rate only when the protocol is serial and `--baud` is omitted. `--user` and `--password` sign in only when the device asks. After `Password:` the line must be quiet briefly before the password and a CR are sent. `Login incorrect` is tried once more. The password is never typed at a `login:` prompt or at a shell prompt (`%`, `#`, `>`, or `$`). A by-id path works as `--serial` or `--host`:

```bash
jackedin connect --protocol serial --host /dev/serial/by-id/usb-Prolific_Technology_Inc._USB-Serial_Controller-if00-port0 --baud 9600
```

### SSH and Telnet

```bash
jackedin connect --host switch.example.net --user admin
jackedin connect --host 192.0.2.10 --trust-host-key --cmd 'show version' --expect '>'
jackedin connect --protocol telnet --host 192.0.2.10 --port 23
```

`--trust-host-key` and `--accept-new` accept a new host key. They do not accept a changed key. On a terminal, the first connection asks `y/N` and shows the fingerprint.

### Command reference

The block below is the program's `--help` text.

```
JackedIN commands
jackedin                     open the window
jackedin --help              show this text and exit (no display needed)
jackedin --version           print the version and exit (no display needed)
jackedin connect --host H [--user U] [--password P] [--key FILE] [--passphrase P]
jackedin connect --host H --trust-host-key [--cmd 'show ver'] [--expect '#']
--cmd runs on an SSH exec channel, so the login banner and the prompt are not included.
jackedin connect --protocol telnet --host 192.0.2.10 --port 23
jackedin connect --protocol serial --host COM5 --port 9600
jackedin connect --protocol serial --serial /dev/ttyUSB0 --baud 9600 --data-bits 8 --parity none --stop-bits 1 --flow none
jackedin ports [--all]         list serial ports (COM and /dev/tty*)
jackedin connect --session "Lab switch" [--cmd 'show ver'] [--expect '#']
jackedin run --session "Lab switch" --cmd 'show ver' --expect '#'
jackedin scan --host H [--ports 22,80,443]
jackedin ping --host H
jackedin trace --host H [--source IP] [--port 22]
jackedin headless            serve the local API (it must be enabled in settings)
jackedin license activate KEY   store an offline license key
jackedin license status         show whether this build is licensed
jackedin eula accept            record acceptance of the license agreement
jackedin eula                   show the agreement file and whether it was accepted
jackedin mcp                 stdio MCP server for the local API (127.0.0.1 only)
jackedin --bench-connect user@host[:port]
jackedin --bench-launch        print ms until the first visible paint, then exit
jackedin --diag-capture        write capture checks and a short start attempt to a file

Serial --host (or --serial / --device) is the device path: COM5 on Windows,
/dev/ttyUSB0 or /dev/serial/by-id/... on Linux. For a serial session, --port is the
baud rate when --baud is omitted. Defaults are 9600 8N1, no flow control.
jackedin ports lists USB and ACM devices first, then the rest in numeric order
(ttyS2 before ttyS10). ttyS ports whose kernel type is 0 are hidden unless --all.
On Linux, permission denied means the user is not in the dialout group (some
systems use uucp or lock). Add the group, then log out and back in.

Logging follows Settings (on by default). --no-log turns it off. --log FILE appends
that file. --raw keeps control codes in the log and on stdout; otherwise CR, NUL,
and escape sequences are stripped. SSH --cmd output is written to that log.

A pipe on stdin is sent to a Telnet session and to an interactive SSH shell.
Example: echo 'show version' | jackedin connect --protocol telnet --host 192.0.2.10
--baud must be a number from 1 to 12000000. A bad value is an error, not 9600.
Serial is assumed when --serial, --device, or --baud is set, or when --host looks
like COM5 or /dev/ttyUSB0, even if --protocol is omitted.
A serial --password is sent only after a Password: prompt has had no new bytes
for a moment. Login incorrect is tried once more. The password is never sent
at a login: prompt. A shell prompt does not receive that password.

SSH reads ~/.ssh/config (Host aliases, HostName, User, Port, IdentityFile, one ProxyJump).
With no --key or --password, ssh-agent (SSH_AUTH_SOCK) is used, then ~/.ssh/id_ed25519,
id_ecdsa, and id_rsa. A host already listed in ~/.ssh/known_hosts is trusted.
The first time a host is seen, a terminal asks y/N. --trust-host-key and --accept-new
accept that new key without a prompt. A changed host key is still refused.

Connect, run, ping, and trace do not need a Pro flag. Scan follows the port scanner flag.
Over HTTP, scan, wait, ping, trace, and the event stream follow the automation API flag.

Commands other than --help and --version require the license agreement.
jackedin eula accept records acceptance. --accept-eula on a command does the same.
The agreement is saved as EULA.txt in the config folder.

A 3-day trial starts when the agreement is first accepted on this computer.
The window, command line, and local API work for 72 hours without a key.
jackedin license status prints the time left. After 72 hours the app locks.

A license key is required after the trial. Buy JackedIN at https://jackedin.app.
jackedin license activate stores the key. A build released
after the key's updates-until date still runs and prints: updates expired, renew.
```

### Flags on `connect`

| Flag | Meaning |
| --- | --- |
| `--host` | SSH or Telnet host. For serial, the device path when `--serial` is omitted. |
| `--port` | TCP port (22 or 23). For serial, the baud rate when `--baud` is omitted. |
| `--user` `--password` `--key` `--passphrase` | SSH credentials. On serial, the password is sent only after a `Password:` prompt. |
| `--protocol ssh\|telnet\|serial` | Default `ssh`. |
| `--session NAME` | Open a saved session by its sidebar name. |
| `--cmd` `--expect` `--timeout` | Run a command and wait for text. SSH `--cmd` uses an exec channel. |
| `--trust-host-key` `--accept-new` | Accept a new host key. |
| `--serial` `--device` | Serial device path (`COM5`, `/dev/ttyUSB0`, `/dev/serial/by-id/...`). |
| `--baud` `--data-bits` `--parity` `--stop-bits` `--flow` | Line settings. Default 9600, 8, none, 1, none. |
| `--log FILE` | Append this log file. |
| `--no-log` | Do not write a session log. |
| `--raw` | Keep NULs, CR, and escape sequences in the log and on stdout. |

## Local API and MCP

The local API is off until you turn it on in Settings. JackedIN listens on `127.0.0.1` only (port 47321 unless you change it) and requires `Authorization: Bearer <token>`. Saving the checkbox starts the listener in the window you already have open. `jackedin headless` serves the same API. Open, send, and close work without the Pro API flag. Scan, wait, ping, traceroute, and the event stream follow that flag.

`jackedin mcp` is a stdio MCP server for that API. It dials 127.0.0.1 only. Leave JackedIN open with the API turned on. The token is `JACKEDIN_API_TOKEN` if that variable is set, otherwise the token saved in Settings. `JACKEDIN_API_PORT` overrides the port. Tools are `list_sessions`, `open_session`, `send_session`, `read_session`, `close_session`, `wait_for_output`, `scan_ports`, `ping_host`, `trace_host`, and `read_events`. The wait, scan, ping, trace, and events tools follow the Pro API flag. `scan_ports` tells the caller to only scan devices they are allowed to test. Example requests are in `docs/openapi.yaml` and `docs/examples/`.

## Where things are stored

The config directory name is `jackedin`, from `brand.json`.

| | Windows | Linux |
| --- | --- | --- |
| Settings and saved sessions | `%APPDATA%\jackedin` | `~/.config/jackedin` |
| Logs | `Documents\JackedIN\Logs` | `~/Documents/JackedIN/Logs` |
| Host keys trusted in the app | inside the settings directory | the same, plus `~/.ssh/known_hosts` |
| Key passphrases | Windows credential store | Secret Service (secret-tool) |
