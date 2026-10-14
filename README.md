# <p style="text-align: center">backup</p>

<p align="center">
  <a href="https://github.com/RogueOneEcho/backup/actions/workflows/ci-on-push.yml"><img alt="CI status" src="https://img.shields.io/github/actions/workflow/status/RogueOneEcho/backup/ci-on-push.yml"></a>
  <a href="https://github.com/RogueOneEcho/backup/releases"><img alt="Latest release" src="https://img.shields.io/github/v/release/RogueOneEcho/backup"></a>
  <a href="LICENSE.md"><img alt="License" src="https://img.shields.io/github/license/RogueOneEcho/backup"></a>
</p>

Backup service data to Backblaze B2 using restic.

```bash
docker pull ghcr.io/rogueoneecho/backup
```

## Features

- Backs up `SOURCE` (default `/srv/${NAME}/`) with configurable exclusions
- Exports SQLite databases safely with integrity checks and `VACUUM INTO`
- Uploads files and database exports as one snapshot to Backblaze B2 via restic with encryption and deduplication
- Automatic retention policy: everything within 14 days, 4 weekly, 12 monthly
- Verifies backup integrity after each run
- Logs progress every 10 seconds; override with `RESTIC_PROGRESS_FPS` (updates per second)

## Build

- amd64 and arm64 images available on [GHCR](https://github.com/RogueOneEcho/backup/pkgs/container/backup)
- Signed with [Cosign](https://github.com/sigstore/cosign) via keyless Sigstore OIDC
- SBOM attestation in CycloneDX format
- Vulnerability scanned with [Grype](https://github.com/anchore/grype)

## Usage

See [docker-compose.yml](docker-compose.yml) for an example.

### Exclusions

Optional `/app/exclude` lists one pattern per line, relative to `SOURCE`:

```
example-1
**/*.log
```

- Lines MUST NOT start with `/`
- Use `**` to match at any depth
- `**` patterns do not skip SQLite databases; databases are only skipped by patterns without `**`

### Restore

Stop the service, remove any leftover `-wal` and `-shm` files, then restore the files and the database exports over them:

```bash
restic restore latest:/srv/test --host test --target /srv/test
restic restore latest:/app/sqlite --host test --target /srv/test
```

## Releases and Changes

Releases and a full changelog are available via [GitHub Releases](https://github.com/RogueOneEcho/backup/releases).
