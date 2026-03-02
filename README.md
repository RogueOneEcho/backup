# <p style="text-align: center">backup</p>

<p align="center">
  <a href="https://github.com/RogueOneEcho/backup/actions/workflows/ci-on-push.yml"><img alt="CI status" src="https://img.shields.io/github/actions/workflow/status/RogueOneEcho/backup/ci-on-push.yml"></a>
  <a href="https://github.com/RogueOneEcho/backup/releases"><img alt="Latest release" src="https://img.shields.io/github/v/release/RogueOneEcho/backup"></a>
  <a href="LICENSE.md"><img alt="License" src="https://img.shields.io/github/license/RogueOneEcho/backup"></a>
</p>

Backup service data to Backblaze B2 using rsync and restic.

```bash
docker pull ghcr.io/rogueoneecho/backup
```

## Features

- Syncs files with rsync and configurable exclusions
- Exports SQLite databases safely with integrity checks
- Uploads to Backblaze B2 via restic with encryption and deduplication
- Automatic retention policy: 5 latest, 7 daily, 4 weekly, 12 monthly
- Verifies backup integrity after each run

## Build

- amd64 and arm64 images available on [GHCR](https://github.com/RogueOneEcho/backup/pkgs/container/backup)
- Signed with [Cosign](https://github.com/sigstore/cosign) via keyless Sigstore OIDC
- SBOM attestation in CycloneDX format
- Vulnerability scanned with [Grype](https://github.com/anchore/grype)

## Usage

See [docker-compose.yml](docker-compose.yml) for an example.

## Releases and Changes

Releases and a full changelog are available via [GitHub Releases](https://github.com/RogueOneEcho/backup/releases).
