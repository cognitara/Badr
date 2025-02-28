# Badr AI Backup System

This document provides comprehensive information about the backup system implemented for the Badr AI Receptionist project.

## Overview

The backup system provides two types of backups:

1. **Local Backups**: Daily backups stored on the local machine
2. **Google Drive Backups**: Weekly backups stored in Google Drive

Both backup types create compressed archives (.tar.gz) of the entire Badr AI project directory.

## Backup Scripts

The following scripts are available in the `scripts` directory:

### 1. local_backup.sh

Creates a local backup of the Badr AI project.

- **Frequency**: Daily at 1:00 AM (when scheduled)
- **Location**: `/home/pi/Backups/Badr/`
- **Retention**: Keeps the 5 most recent backups
- **Log File**: `/home/pi/local_backup.log`

**Manual Execution**:
```bash
./scripts/local_backup.sh
```

### 2. gdrive_backup.sh

Creates a backup and uploads it to Google Drive.

- **Frequency**: Weekly on Sunday at 2:00 AM (when scheduled)
- **Location**: Google Drive folder `BadrBackups`
- **Account**: info.cognitrara@gmail.com
- **Log File**: `/home/pi/gdrive_backup.log`

**Manual Execution**:
```bash
./scripts/gdrive_backup.sh
```

### 3. backup.sh

Master script that runs both local and Google Drive backups.

**Manual Execution**:
```bash
./scripts/backup.sh
```

### 4. verify_backups.sh

Verifies the integrity of both local and Google Drive backups.

- **Frequency**: Daily at 3:00 AM (when scheduled)
- **Log File**: `/home/pi/verify_backup.log`

**Manual Execution**:
```bash
./scripts/verify_backups.sh
```

### 5. setup_backup_cron.sh

Sets up automated backup schedule using cron.

**Manual Execution**:
```bash
./scripts/setup_backup_cron.sh
```

## Initial Setup

### 1. Google Drive Setup

Before using Google Drive backups, you need to configure rclone:

1. Install rclone:
   ```bash
   sudo apt install rclone
   ```

2. Configure rclone for Google Drive:
   ```bash
   rclone config
   ```

3. Follow the prompts:
   - Choose `n` for new remote
   - Name: `badr_gdrive`
   - Type: `drive`
   - Client ID: (leave blank)
   - Client Secret: (leave blank)
   - Scope: `1` (full access)
   - Root folder ID: (leave blank)
   - Service account file: (leave blank)
   - Auto config: `y`
   - Team drive: `n`

4. A browser window will open. Log in with info.cognitrara@gmail.com and grant access.

### 2. Set Up Automated Backups

Run the setup script to configure automated backups:

```bash
./scripts/setup_backup_cron.sh
```

This will set up the following schedule:
- Local backup: Daily at 1:00 AM
- Google Drive backup: Weekly on Sunday at 2:00 AM
- Backup verification: Daily at 3:00 AM

## Backup Restoration

### Restoring from Local Backup

1. Find the backup file in `/home/pi/Backups/Badr/`
2. Extract the backup:
   ```bash
   tar -xzf /home/pi/Backups/Badr/badr_backup_YYYYMMDD_HHMMSS.tar.gz -C /path/to/restore
   ```

### Restoring from Google Drive Backup

1. List available backups:
   ```bash
   rclone ls badr_gdrive:BadrBackups
   ```

2. Download the backup:
   ```bash
   rclone copy badr_gdrive:BadrBackups/badr_backup_YYYYMMDD_HHMMSS.tar.gz /tmp/
   ```

3. Extract the backup:
   ```bash
   tar -xzf /tmp/badr_backup_YYYYMMDD_HHMMSS.tar.gz -C /path/to/restore
   ```

## Troubleshooting

### Local Backup Issues

- Check disk space: `df -h`
- Check backup log: `cat /home/pi/local_backup.log`
- Verify backup directory exists: `ls -la /home/pi/Backups/Badr/`

### Google Drive Backup Issues

- Check rclone configuration: `rclone config show badr_gdrive`
- Test rclone connection: `rclone lsd badr_gdrive:`
- Check backup log: `cat /home/pi/gdrive_backup.log`
- Verify internet connection: `ping -c 4 google.com`

### Cron Job Issues

- Check if cron is running: `systemctl status cron`
- View cron jobs: `crontab -l`
- Check system logs: `grep CRON /var/log/syslog`

---

Powered by Cognitara (c) 2025
