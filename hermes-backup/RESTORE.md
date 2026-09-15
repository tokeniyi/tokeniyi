# Hermes Configuration Restore Guide

This repository contains automated backups of the Hermes configuration.

## Restoring from `latest_backup.tar.gz`

### Prerequisites

- Hermes Agent installed and running
- Access to the target environment (same user/context as the backup)

### Steps

1. **Extract the archive**

   ```bash
   tar -xzf latest_backup.tar.gz
   ```

   This will create a directory structure with backed-up files.

2. **Restore skills**

   - Navigate to the extracted `skills/` directory
   - For each `SKILL.md` file, review the procedure
   - Use `skill_manage` or the Hermes interface to import/recreate skills
   - Or copy the `skills/` directory contents to the target Hermes `skills/` folder

3. **Restore memories**

   - Navigate to the extracted `memories/` directory
   - Review `user` and `memory` entries
   - Import relevant facts into the target Hermes memory store
   - Use the `memory` tool to add entries if needed

4. **Restore cron jobs**

   - Navigate to the extracted `cron/` directory
   - Review scheduled job configurations
   - Re-create cron jobs via the Hermes gateway or `cronjob_manage` tool
   - Ensure the cron schedule matches your needs

5. **Restore platform settings**

   - Navigate to the extracted `platform/` directory
   - Review profile configurations, environment settings
   - Apply to the target Hermes instance
   - May require manual re-configuration of some settings

6. **Verify restoration**

   - Check that all skills are accessible via `skill_view()`
   - Verify memories are injected correctly
   - Test that cron jobs trigger as expected
   - Confirm platform settings are as expected

### Post-Restoration

- Run `hermes-agent verify` (if available) to check configuration integrity
- Review recent sessions to ensure nothing was missed
- Update any credentials or secrets that may not have been backed up

## What's NOT backed up

- **Secret credentials** (API tokens, passwords, API keys) — never stored in this repo
- Temporary session data
- Runtime state (active processes, live connections)
- User-specific data outside Hermes configuration

## Backup Verification

After restoring, verify:

| Check | Method |
|---|---|
| Skills list | `skill_view(name='...')` for each expected skill |
| Memories | `memory` store entries match expected profile |
| Cron jobs | Visible in Hermes gateway cron interface |
| Platform | Active profile matches expected configuration |

## Troubleshooting

- If skills fail to import, check the `SKILL.md` frontmatter for required dependencies
- If memories don't restore, verify the `user` profile identifiers match
- If cron jobs don't trigger, check the gateway cron configuration
- For persistent issues, consult the Hermes documentation at https://hermes-agent.nousresearch.com/docs
