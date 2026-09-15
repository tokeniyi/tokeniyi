# Hermes Backup Repository

Private backup of Hermes configuration: skills, memories, cron jobs, platform settings.

## About

This repository contains weekly backups of the Hermes Agent configuration, including:
- Skills (procedures, workflows, automations)
- Memories (user profile, session notes, standing conventions)
- Cron jobs (scheduled tasks, daily/weekly automations)
- Platform settings (configurations, environment, profiles)

## Backup Schedule

Backups are created **weekly on Sunday at 2 AM** via Hermes cron job.

The `latest_backup.tar.gz` archive contains a complete snapshot of the backup at the time of creation.

## Restoration

See `RESTORE.md` for detailed restoration instructions.

## Contents Backup

Each backup includes (but is not limited to):

| Item | Description |
|---|---|
| `skills/` | All SKILL.md files and procedures |
| `memories/` | User profile and session notes |
| `cron/` | Scheduled task configurations |
| `platform/` | Platform settings and environment |
| `.hermes/` | Hermes runtime configuration |

## Usage

### To restore from a backup:

1. Download or clone this repository
2. Follow the restoration guide in `RESTORE.md`
3. Ensure the target Hermes instance is properly configured
4. Verify all skills, memories, and cron jobs are intact

### To create a new backup:

1. Ensure all configuration is up to date
2. Run the Hermes backup cron job
3. The `latest_backup.tar.gz` will be updated automatically
4. Commit the new archive to this repository
