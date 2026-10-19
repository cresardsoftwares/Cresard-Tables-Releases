# Cresard Tables — releases

**Download the latest Cresard Tables**, or read the notes below and pick a file.

This repository holds release artefacts only. It has no source code — the source repository is
private, and this one exists so that anyone can download a build without having access to it.

| Download | File | Size |
|---|---|---|
| **Cresard Tables Setup** — the installer, Windows x64 | [`cresard-tables-windows-x64.msi`](dist/cresard-tables-windows-x64.msi) | ~14 MB |
| **Portable** — the app and the CLI in one folder, Windows x64 | [`cresard-tables-windows-x64-portable.zip`](dist/cresard-tables-windows-x64-portable.zip) | ~18 MB |
| Checksums for every file | [`SHA256SUMS.txt`](dist/SHA256SUMS.txt) | |
| Version, date and release notes | [`version.json`](dist/version.json) | |

Those links always point at the newest build; `dist/version.json` says which version that is. Older
builds stay in this repository's history (`git log -- dist/`).

- **Product page:** <https://desk.cresard.com/tables>
- **Website:** <https://cresard.com>

## Install

**Installer:** download `cresard-tables-windows-x64.msi` and run it. Setup ("Cresard Tables Setup")
puts the app and the command-line tool in Program Files, adds a Start menu entry, offers a desktop
shortcut and unregisters cleanly from *Settings → Apps*.

**Portable:** download `cresard-tables-windows-x64-portable.zip`, unzip it anywhere and run
`cresard-tables.exe`. Nothing is written outside that folder.

Neither build installs a service or a background updater. The builds are not code-signed yet, so
Windows SmartScreen may show a warning the first time — choose *More info → Run anyway* if you are
comfortable with that, after checking the checksum below.

Folder after unzipping:

```
cresard-tables-windows-x64/
  cresard-tables.exe        the app
  cresard-tables-cli.exe    the command-line tool
  README.md                 what the app is and what it can do
  NOTICE, LICENSE-MIT, LICENSE-APACHE, ATTRIBUTION.md
```

**Requirements:** Windows 10 or later, 64-bit. Nothing else: the build links the C runtime
statically, so no Visual C++ redistributable is needed. Everything the app writes stays in
`%APPDATA%\Cresard Tables` — delete that folder and the app is gone.

**If the app doesn't open:** the app uses DirectX 12 by default, and some graphics drivers cannot
start it. From the folder containing the executable:

```powershell
$env:WGPU_BACKEND = "vulkan"
& .\cresard-tables.exe
```

`vulkan`, `gl` and `dx12` are the values to try. The log in `%APPDATA%\Cresard Tables\logs` records
which renderer was chosen.

## Verify before you run it

Every file's SHA-256 is in [`dist/SHA256SUMS.txt`](dist/SHA256SUMS.txt):

```powershell
Get-FileHash .\cresard-tables-windows-x64-portable.zip -Algorithm SHA256
```

The hash must match the line for that file. If it does not, do not run it — download it again.

## What is in this repository

```
dist/                     the current build, its checksums and version.json
  cresard-tables-windows-x64-portable.zip
  SHA256SUMS.txt
  version.json
  NOTICE                  required notices
  LICENSE-MIT             MIT licence
  LICENSE-APACHE          Apache-2.0 licence
  ATTRIBUTION.md          every bundled asset and its licence
  cresard-tables.ico      the app icon, for store listings
README.md                 this file
```

The files are published by hand over the Cresard SSH key; there is no CI and no token that can
write here. Each publish is a single commit, tagged `v<version>`.

## Licence

Cresard Tables is free software, dual-licensed under the [MIT licence](dist/LICENSE-MIT) or
[Apache-2.0](dist/LICENSE-APACHE), at your option. Copyright (c) 2026 Cresard Desk Team and the
Cresard Tables contributors. It is a rebranded distribution of [GridCraft](https://github.com/storytold/gridcraft),
Copyright (c) 2026 ArtCraft Team and the GridCraft contributors, and both copyright notices are kept
in full as the licence requires. The notices travel with every build; see [`dist/NOTICE`](dist/NOTICE).

The **Cresard Desk** and **Cresard Tables** names, the wordmark and the app icon are trademarks of
Cresard Desk. They are not covered by the software licence, and a modified build must not use them.

<sub>Microsoft, Excel and Microsoft 365 are trademarks of Microsoft Corporation. Cresard Tables is an
independent project and is not affiliated with, sponsored by or endorsed by Microsoft Corporation;
those names describe the workflows it is compatible with.</sub>

## Support

- Bug reports, questions and feature requests: <contact@cresard.com>
- Product page: <https://desk.cresard.com/tables>
- Follow along: [X](https://x.com/cresard) · [LinkedIn](https://www.linkedin.com/company/cresard) · [GitHub](https://github.com/cresard)

Cresard Tables is in **alpha**. It works, and it can lose your work. Keep a copy of anything you
care about, and tell us what breaks.
