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

Compare it with the published value. Releases also carry a
[build provenance attestation](https://docs.github.com/actions/security-guides/using-artifact-attestations),
so you can confirm the binary was built by the release workflow rather than
uploaded by hand:

```bash
gh attestation verify Stayaway_0.1.0_x64-setup.exe --owner meharsulaiman
```

## About the Windows warning

These builds are **not yet signed with an Authenticode certificate**, so
SmartScreen will warn that the publisher is unrecognised, and some antivirus
software may flag them. That is expected for a new, unsigned application, and
the checksum and attestation above are how you can check the download is the
one this workflow produced.
