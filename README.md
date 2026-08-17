# MeshDrop Releases

Release artifacts for the MeshDrop auto-updater. This repository hosts the
built binaries and update manifests that the desktop and mobile apps check
for new versions.

**Do not clone this repo for development** — it contains only CI-published
artifacts. For source code, see the repos below.

## Ecosystem

| Repository | Visibility | Contents |
|------------|-----------|----------|
| [meshdrop-app](https://github.com/aamirali51/meshdrop-app) | Private | Desktop + mobile clients |
| [meshdrop-core](https://github.com/aamirali51/meshdrop-core) | Public | P2P engine — `@mesh/core` |
| **meshdrop-releases** (this repo) | Public | Release artifacts for the auto-updater |

## What's here

Each [GitHub Release](https://github.com/aamirali51/meshdrop-releases/releases)
contains the following artifacts for the latest version:

| Artifact | Platform | Description |
|----------|----------|-------------|
| `MeshDrop-Setup-<ver>.exe` | Windows | NSIS installer |
| `MeshDrop-<ver>-portable.exe` | Windows | Single-file portable executable |
| `MeshDrop-<ver>-mac-arm64.dmg` | macOS | Apple Silicon disk image |
| `MeshDrop-<ver>-linux-x86_64.AppImage` | Linux | Portable Linux binary |
| `MeshDrop-<ver>.apk` | Android | React Native release APK |
| `latest.yml` | Windows | Electron-updater manifest |
| `latest-mac.yml` | macOS | Electron-updater manifest |
| `latest-linux.yml` | Linux | Electron-updater manifest |
| `latest.json` | Android | In-app updater manifest |

## How updates work

- **Desktop** — electron-updater checks `latest.yml` / `latest-mac.yml` / `latest-linux.yml`
  from this repo's public releases. The `RELEASES_PAT` secret in `meshdrop-app`
  allows the CI workflow to upload artifacts here.
- **Mobile** — The Android app fetches `latest.json` and compares the
  `versionName` field to the installed version.
- **Portable builds** — Optionally signed with `MESHDROP_UPDATE_KEY` (ed25519).
  The `.sig` files provide integrity verification; unsigned portable builds
  refuse self-updates.

## How artifacts get here

Artifacts are published automatically by the
[meshdrop-app CI workflow](https://github.com/aamirali51/meshdrop-app/actions)
when a `v*` tag is pushed. Do not upload artifacts manually.
