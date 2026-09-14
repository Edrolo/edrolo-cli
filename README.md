# Edrolo CLI

`edrolo` is a command-line client for the Edrolo API: exams, courses and
lessons, question search, timetable and class mapping, and school user
management.

This repository publishes the **releases**. The source lives in a private
repository; the binaries here are public so Homebrew and winget can fetch them
without authentication. The winget manifests live here too, under
[`manifests/`](manifests).

## Install

**macOS / Linux — Homebrew**

```bash
brew install edrolo/edrolo/edrolo
```

**Windows — winget**

The package is not in the public winget index, so install from the manifest in
this repository rather than by name:

```powershell
# once per machine: local manifests are disabled by default
winget settings --enable LocalManifestFiles     # run as Administrator

git clone --depth 1 https://github.com/Edrolo/edrolo-cli
winget install --manifest .\edrolo-cli\manifests\e\Edrolo\EdroloCLI\<version>
```

`--manifest` takes the **directory** holding the three YAML files, not one of
them. `winget install Edrolo.EdroloCLI` by name will not resolve.

**Any platform — direct download**

Grab the archive for your OS and architecture from
[Releases](../../releases), check it against `SHA256SUMS`, and put `edrolo` on
your `PATH`.

## Getting started

```bash
edrolo login          # opens a browser, stores the token (defaults to prod)
edrolo whoami         # confirms the stored credential still works
edrolo agent-help     # the full command guide, including the sharp edges
```

`edrolo --help` lists the command groups. Read `agent-help` before automating
anything: it documents which commands replace whole content trees and which
send real email.

## Two things to know before you use it in anger

**Some commands delete more than they appear to.** `courses update` and
`lessons update` replace an entire tree — any topic, lesson or chunk absent
from the payload is deleted server-side. Both fetch the current state first and
refuse a destructive payload unless you pass `--confirm`, naming exactly what
would go. Use `--dry-run` to see it without writing.

**Some commands email real people.** Several `edrolo users` commands send
genuine, irreversible email to students, teachers and guardians in whatever
environment you are pointed at, production included. Each refuses without
`--confirm` and states how many recipients would be mailed. `--dry-run` shows
who, and sends nothing.

Output from the `classes` and `users` groups masks email addresses and surnames
by default, in every format. Pass `--show-pii` when you genuinely need the real
values.

## macOS: "cannot be opened because the developer cannot be verified"

Release binaries are not yet signed or notarized. Installing via Homebrew avoids
this — the Cask clears the quarantine attribute. A binary downloaded directly
will be blocked by Gatekeeper until you clear it yourself:

```bash
xattr -d com.apple.quarantine /path/to/edrolo
```

## Support

Please raise an [issue](../../issues).
