# Backup

Docker container for backing up service data to Backblaze B2 using rsync and restic.

## Features

- Syncs files using rsync with configurable exclusions
- Exports SQLite databases safely with integrity checks
- Uploads to Backblaze B2 using restic (encrypted, deduplicated)
- Automatic retention policy (7 daily, 4 weekly, 12 monthly)
- Verifies backup integrity after each run

## Environment Variables

| Variable | Description |
|----------|-------------|
| `NAME` | Backup name (used for restic host and repo path) |
| `SOURCE` | Source directory to backup (default: `/srv/${NAME}/`) |
| `B2_APPLICATION_KEY` | Backblaze B2 application key |
| `B2_APPLICATION_KEY_ID` | Backblaze B2 application key ID |
| `B2_BUCKET` | Backblaze B2 bucket name |
| `RESTIC_PASSWORD` | Restic repository encryption password |

## Usage

### With Docker Compose

```yaml
services:
  backup-myservice:
    image: ghcr.io/rogueoneecho/backup:latest
    userns_mode: host
    environment:
      NAME: myservice
    env_file:
    - .env
    configs:
    - source: myservice_backup_exclude
      target: /app/exclude
    volumes:
    - /srv/myservice:/srv/myservice:ro
    - /srv/shared/backups/myservice:/srv/shared/backups/myservice
    - /srv/shared/backups/.restic-cache:/root/.cache/restic

configs:
  myservice_backup_exclude:
    content: |
      cache
      logs
```

### Running

```bash
docker compose run --rm backup-myservice
```

## Testing

```bash
docker compose run --rm backup-test
```

## Exclusions

Create an exclusion file mounted at `/app/exclude`. Patterns match path components (not substrings).

Example:
```
cache
logs
temp
```
