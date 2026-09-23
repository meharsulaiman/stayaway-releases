# Stayaway — downloads

Build artifacts for [Stayaway](https://stayaway.app), which keeps your computer
active while you step away.

**This repository holds no source code.** It exists so the installer and the
update feed have a public home: the app's updater fetches from here, and an
updater cannot authenticate to a private repository.

## What is here

| | |
|---|---|
| **Releases** | the Windows installer, its signature, and a SHA-256 checksum |
| `latest.json` | the update feed the installed app reads |

## Verifying a download

Every release publishes a `.sha256` beside the installer. On Windows:

```powershell
Get-FileHash .\Stayaway_0.1.0_x64-setup.exe -Algorithm SHA256
```

Compare it with the published value. If they differ, do not run the file.

The `.sig` file beside it is **not** for you to check by hand — it is what the
installed app verifies before applying an update, against a public key compiled
into the application itself. That is the mechanism that stops anyone who can
serve you a file from serving you a different one.

## About the Windows warning

These builds are **not signed with an Authenticode certificate**, so SmartScreen
will warn that the publisher is unrecognised, and some antivirus software may
flag them. That is expected for a new, unsigned application: reputation accrues
to a signing identity, and an unsigned binary has none to accrue.

The checksum above is how you can confirm the download is the file this project
published.
