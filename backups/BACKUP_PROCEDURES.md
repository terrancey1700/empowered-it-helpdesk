# Backup Procedures – Database & Application Files

## Objective

Protect helpdesk data by backing up:

- MariaDB database (`helpdesk_db`)
- Application files (`/var/www/helpdesk`)

Backups ensure recovery if the server fails, is compromised, or misconfigured.

---

## Why This Step Matters

- The database contains ticket history and user data.
- The application folder contains configuration files and attachments.
- Without backups, ticket data could be permanently lost.

---

## Step 1 – Gain Proper Privileges

Switched to root shell:

sudo -i

Purpose:

Some backup operations require elevated privileges.

---

## Step 2 – Create Database Backup

mysqldump helpdesk_db > helpdesk_backup.sql

Purpose:

Creates a full SQL dump of the helpdesk database.

This file can later be restored into MariaDB if needed.

---

## Step 3 – Backup Application Files

tar -czvf helpdesk_files_backup.tar.gz /var/www/helpdesk

Purpose:

Creates compressed archive of:

- osTicket application files
- Configuration files
- Attachments

---

## Step 4 – Store Backups Safely

Backups stored outside the web directory.

Purpose:

- Prevent public web access to backups.
- Reduce exposure of sensitive data.

---

## Issues Encountered

### Permission Denied Errors

Attempted to write backups into restricted directories without proper privileges.

Resolution:

Used sudo -i to operate as root when required.

---

## Lessons Learned

- `/root` is private and not accessible to standard users.
- Always verify current user context before running commands.
- Backups must not be stored inside the public web directory.

---

## Final State

- Database backup procedure established
- Application file backup procedure established
- Permission issues resolved
- Basic data protection process documented
