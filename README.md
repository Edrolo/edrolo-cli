# Edrolo CLI

`edrolo` is a command-line client for the Edrolo API: exams, courses,
lessons, question search, timetable and class mapping, and school user
management.

This repository exists to **publish the releases**. The source lives in a
private repository; the binaries here are public so that Homebrew and winget
can download them without authentication.

## Install

**macOS / Linux (Homebrew)**

```bash
brew install edrolo/edrolo/edrolo
```

**Windows (winget)**

```powershell
winget install Edrolo.EdroloCLI
```

**Any platform** — download the archive for your OS and architecture from
[Releases](../../releases), verify it against `SHA256SUMS`, and put `edrolo`
on your `PATH`.

## Getting started

```bash
edrolo login --env prod     # opens a browser, stores the token
edrolo whoami               # confirms the credential works
edrolo agent-help           # the full command guide
```

## Support

Please raise an [issue](../../issues).

## A note on macOS

Release binaries are not yet signed or notarized, so a **directly downloaded**
macOS binary is blocked by Gatekeeper. Installing via Homebrew avoids this.
