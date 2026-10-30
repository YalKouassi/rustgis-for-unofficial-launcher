# RustGIS for Craft Unofficial Launcher

**An unofficial mirror** of [RustGIS](https://github.com/opengeos/RustGIS) releases, maintained by
[YalKouassi](https://github.com/YalKouassi), so that
[Craft Unofficial Launcher](https://github.com/YalKouassi/craft-unofficial-launcher) can install
and update RustGIS.

This repo is **not affiliated with, endorsed by or supported by Open Geospatial Solutions** (the authors of RustGIS),
**or by ArtCraft**. Report problems with RustGIS itself upstream at
<https://github.com/opengeos/RustGIS>; report problems with this mirror here.

## What this repo publishes

The packages in this repo's releases are **RustGIS's own builds**, as published on
[opengeos/RustGIS's releases](https://github.com/opengeos/RustGIS/releases). Nothing is rebuilt and no program file is
changed. Each release here:

- downloads upstream's packages and verifies each one before using it;
- renames them to the launcher's `<id>-<version>-<os>-<arch>` naming and, only where the launcher
  couldn't install an archive's layout, repacks that archive (the same files with the same bytes,
  in different folders);
- adds `craft-app.json`, the icon, `SHA256SUMS.txt`, and upstream's licence files from the same tag.

The notes of each release list every file, the upstream asset it came from, its SHA-256, and
whether it was repacked, so you can compare it with upstream's release.

### For RustGIS

Upstream's packages are **renamed** to the launcher's naming contract and otherwise mirrored
**byte for byte**:

| Upstream | Here |
|---|---|
| `RustGIS-<v>-windows-x86_64-portable.zip` | `rustgis-<v>-windows-x64-portable.zip` |
| `RustGIS-<v>-windows-x86_64.msi` | `rustgis-<v>-windows-x64.msi` |
| `RustGIS-<v>-linux-<arch>.AppImage` / `.tar.gz` | `rustgis-<v>-linux-<arch>.AppImage` / `.tar.gz` |
| `RustGIS-<v>-macos-<arch>.dmg` | `rustgis-<v>-macos-<arch>.dmg` |
| `rustgis-<v>-1.<arch>.rpm` | `rustgis-<v>-linux-<arch>.rpm` |
| `rustgis_<v>_amd64.deb` / `_arm64.deb` | `rustgis-<v>-linux-x86_64.deb` / `-linux-aarch64.deb` |

Every download is checked against upstream's `SHA256SUMS` first. The icon is the 512 px
`rustgis.png` from upstream's Linux tarball.

Not mirrored: the Python wheels, the `.msix` and `-setup.exe` installers (the launcher installs the MSI and the portable zip), the `.zsync` files, the source tarball and the CLI-only macOS builds.

## How it runs

[`.github/workflows/bridge.yml`](.github/workflows/bridge.yml) runs every 30 minutes. It uses
[craft-bridge](https://github.com/YalKouassi/craft-bridge) with [`bridge.toml`](bridge.toml) to
check upstream's latest release and mirror it if this repo doesn't have it yet. If upstream starts
publishing its own `craft-app.json`, the bridge stops publishing, and the launcher should point at
upstream directly.

Using this mirror means trusting its maintainer as well as upstream; see
[craft-bridge's Trust section](https://github.com/YalKouassi/craft-bridge#trust).

## Licences

RustGIS is licensed by its authors under Apache-2.0; each release attaches upstream's licence files.
This repo's own files (the config, workflow and this README) are available under MIT OR
Apache-2.0 ([LICENSE-MIT](LICENSE-MIT), [LICENSE-APACHE](LICENSE-APACHE)).
