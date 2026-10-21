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

