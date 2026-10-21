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

