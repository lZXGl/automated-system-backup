# Universal Automated Backup Utility

A lightweight, zero-dependency Python snapshot backup tool for Linux servers, homelabs, and development workstations. Creates compressed archives of specified directories and automatically enforces rolling retention policies.

## ✨ Features

- **Zero Third-Party Dependencies**: Pure Python 3 standard library (`tarfile`, `shutil`, `argparse`).
- **Flexible Compression**: Supports `gz` (gzip), `bz2` (bzip2), and uncompressed archives.
- **Smart Retention Management**: Prunes backups older than a specified number of days (`--retention-days`) or exceeding a maximum archive count (`--keep-count`).
- **Smart Exclusion**: Preconfigured to skip noise directories (`__pycache__`, `node_modules`, `.git`, `.venv`, temp files).
- **Dry-Run Safe**: Preview archiving and deletion actions without modifying files.

## 🚀 Usage

### Simple Backup
```bash
python3 backup_task.py --source /path/to/data --destination /backups
```

```text
$ python3 backup_task.py --source /opt/configs --destination /backups --verbose
[2026-09-20 03:00:01] Archiving /opt/configs -> /backups/backup_configs_20260920_030001.tar.gz
[2026-09-20 03:00:04] Archive created: 18.4 MB (SHA256: e3b0c44298fc1c149afbf4c8...)
[2026-09-20 03:00:04] Enforcing retention policy: 7 days retention, 10 archives max
[2026-09-20 03:00:04] Backup cycle completed successfully.
```

### Multiple Directories with 14-day Retention
```bash
python3 backup_task.py \
  --source /etc/nginx /opt/configs \
  --destination /var/backups/homelab \
  --retention-days 14 \
  --keep-count 20
```

### Test via Dry Run
```bash
python3 backup_task.py --source . --destination ./backups --dry-run --verbose
```

### Automated Cron Job (Daily at 3 AM)
```bash
0 3 * * * /usr/bin/python3 /path/to/backup_task.py --source /home/user/data --destination /backup/daily --retention-days 7 >> /var/log/backup.log 2>&1
```

## 📄 License
MIT License.