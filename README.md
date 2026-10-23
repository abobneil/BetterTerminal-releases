# BetterTerminal

BetterTerminal is a Windows desktop PowerShell console for sysadmins who work on several hosts at once. Run
commands locally or over WinRM or SSH, and see the output as searchable tables, service and system cards and
charts alongside live host metrics.

This repository publishes BetterTerminal's releases and the feed installed copies use to update themselves.
It contains no source code.

## Install

Download `BetterTerminal-<version>-x64-setup.exe` from the
[latest release](https://github.com/abobneil/BetterTerminal-releases/releases/latest) and run it. It needs
Windows 10 version 1809 or later, or Windows 11, on x64, and installs Microsoft Edge WebView2 Runtime if it
is missing. A portable zip is attached to each release as well; it needs WebView2 Runtime already installed.

Installed copies update themselves: use the update button in the title bar, or **Check for updates** in the
command palette (Ctrl+Shift+P). The installer and app are unsigned. `SHA256SUMS.txt` in each release lists
the SHA-256 of every download.

## Release notes

### 1.8.0 - 2026-10-23

#### Changed

- Each session detail now appears once, giving the timeline more room. The tab names the computer, the bar above the charts shows how you're connected along with the OS, shell version, user and uptime, and the working directory moves into the prompt itself, as in PowerShell.
- The local tab and command cards show the computer's name instead of "localhost".
- Incident recording sits in the bar above the charts instead of taking a row of its own, and the 15m/30m/60m range and the collapse and expand buttons sit beside the chart's time axis.
- Sessions, Disconnect, sign-in settings and End session are in the menu on the connection pill (Local, WinRM, SSH). The new-tab menu also offers Manage sessions.
- The alerts bell shows a count only when other tabs have alerts; the active tab's badge already shows its own.

### 1.7.0 - 2026-10-23

#### Added

- Linux bash tabs can switch users with `sudo su`, `sudo -i`, and related shell commands. Subsequent commands and the prompt use the selected user until `exit`; nested switches restore the previous directory and exports. Persistent helper sessions retain the switched user when resumed.

#### Fixed

- Stopping a command in a bash tab keeps the shell alive when it handles the interrupt, including while switched to another user. Ending a helper session also stops switched shells and their terminal programs.
- Resuming a helper session no longer logs duplicate history inserts, and ending active work no longer reports a stale alert refresh as an engine failure.

### 1.6.1 - 2026-10-23

#### Fixed

- Command, script and runbook cards no longer show an empty output box while running silently or after finishing without output.

### 1.6.0 - 2026-10-23

#### Changed

- Session controls now share the host, working directory and shell information row above the command entry, leaving more room for command output. They wrap when the window is narrow.

#### Fixed

- Brief Windows file locks no longer interrupt saving persistent sessions during connect or reconnect.
- Resuming or ending a disconnected WinRM session now uses its original account and offers fresh credentials when Windows cannot reuse the saved logon context, without deleting the saved password or changing the host's sign-in setting.
- Session errors display readable messages instead of raw WinRM XML, and errors already shown in a session dialog no longer also appear as oversized notifications.

### 1.5.0 - 2026-10-22

#### Added

- Remote connections now offer persistent sessions that keep shell state and running work through app closure or a network drop. Choose native WinRM persistence without installing anything, an optional per-user session helper, or a temporary session. Helper setup asks for permission and can provision its own verified runtime.
- A Sessions button above the command entry lets you find, switch, resume, and create sessions on the same host. Disconnect keeps persistent sessions available; End session explicitly stops their work and discards shell state.

#### Fixed

- First-connect sign-in settings now open in a floating dialog instead of appearing inside the command timeline.

### 1.4.0 - 2026-10-22

#### Added

- `ifconfig` on a Linux or macOS server now shows each interface as a card, with its address, prefix and MAC
  address, and its flags, MTU, traffic and any errors or drops when you open it. This also works for the
  older BusyBox layout in Alpine containers. `ifconfig -s` shows packet counters for each interface, the same
  way `netstat -i` does.
- Tab completion now works in bash sessions over SSH. Press Tab or Ctrl+Space to complete commands, file and
  folder paths, options, `$` variables, and arguments such as `systemctl` units, `git` subcommands or `apt`
  packages, using the completions installed on the server. Names with spaces are escaped for you, and it
  works while a command is still running.
- Choose how you sign in to each server. The first connection to a server always uses its password. After
  that you can pick a password each time, a saved password, or an SSH key that BetterTerminal creates for that
  server alone, and change it later from **Host settings**. Windows servers can use SSH keys too: BetterTerminal
  can turn on OpenSSH Server and PowerShell remoting over SSH for you (PowerShell 7 must be installed).
- SSH keys are rotated automatically on a schedule you set (90 days by default, adjustable per server, with an
  optional machine-wide limit). A due key is replaced the next time you connect, and **Rotate now** does it on
  demand.
- On Linux servers, `sudo` can use a saved sudo password, or a passwordless sudo rule that BetterTerminal
  installs and checks for you, so elevated commands don't keep asking.
- Servers that refuse passwords can still be connected the first time by confirming that your existing SSH
  keys should be used.

#### Changed

- `top -b` output on a Linux server now shows the same process card as `ps`: the top memory and CPU users with
  the full list behind **Show all**, or a bar chart when you sort with `-o %MEM` or `-o %CPU`. The load, CPU
  and memory summary lines are no longer shown on the card.
  `top`, `htop` and `btop` on their own still open full-screen as before.

#### Security

- Saved passwords and SSH keys are now kept in an encrypted vault protected by the PC's TPM and Windows Hello,
  or by a master password on PCs without them. SSH keys never leave the TPM unencrypted, and each key only
  works with the server it was made for. Passwords saved by earlier versions move into the vault the first
  time you unlock it.

### 1.2.0 - 2026-10-21

#### Added

- Connect to Linux servers over SSH with a normal bash shell. Choose **SSH** in the new-session dialog and enter
  `user@host` or a host alias from your SSH config. Your SSH config, agent and keys are used, and BetterTerminal
  asks for a password or passphrase only when needed. Unknown host keys ask for confirmation, and a changed host
  key is always refused.
- Linux tabs keep your working folder and exported variables between commands, stop commands with Ctrl+C, ask for
  your sudo password when a command needs it, and open full-screen programs such as `top`, `htop`, `vim` and
  `less` in a terminal card.
- Linux tabs have the metrics strip, top consumers, file manager (over SFTP), file transfers and alerts for failed
  services, full disks and pending reboots.
- Cards for everyday Linux commands, including `ps`, `top`, `pstree`, `ip`, `ss`, `ping`, `traceroute`, `dig`,
  `systemctl`, `journalctl`, `df`, `du`, `lsblk`, `free`, `fdisk`, LVM, `apt`, `dpkg`, `ufw`, `iptables`, `nft`,
  `fail2ban`, `docker`, `last`, `sudo -l`, `crontab`, `ls -l`, `grep`, `find`, web server access logs and
  `curl -v`.
- Any command that prints JSON gets a collapsible, searchable JSON view.

#### Changed

- The new-session dialog offers **WinRM**, **SSH** and **PowerShell over SSH**. The previous SSH option, which
  needs PowerShell on the server, is now called PowerShell over SSH.

### 1.1.0 - 2026-10-21

#### Added

- Feedback on cards. Each command, terminal and script card has a feedback button where you can say how
  useful the card was or how its formatting could be better, rate it, and paste or attach screenshots.
  Feedback goes to the developers privately. The command and its output are left out unless you choose to
  include them after reviewing a preview.

### 1.0.5 - 2026-10-20

#### Fixed

- Follow-up questions to Codex in Ask AI no longer fail when the session's working folder isn't a Git repository.

### 1.0.4 - 2026-10-20

#### Added

- In-app updates. Installed copies check for new versions and show available updates in the title bar and
  under **Check for updates** in the command palette. The update downloads, is checked against its published
  SHA-256 and installs silently, then BetterTerminal reopens. Portable copies link to the release page.
  This version has to be installed by hand; later versions arrive in the app.

### 1.0.3 - 2026-10-20

#### Added

- The title bar shows the installed app version.

#### Changed

- Releases are built and published automatically, with a `SHA256SUMS.txt` covering every download.
- Updated third-party dependencies.

### 1.0.2 - 2026-10-20

First published release: local, WinRM and SSH tabs, live host metrics, the command timeline with visual
output cards, paste-as-cards with the offline HTML viewer, alerts and Windows updates, the file manager and
viewer, the script and runbook library, incident recording, Ask AI with Claude Code or Codex, and the
command palette.

