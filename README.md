# Empowered IT Helpdesk Deployment
## Production osTicket Deployment on Ubuntu VPS

End-to-end deployment of a cloud-hosted IT helpdesk system using Ubuntu, Apache, PHP, MariaDB, Let’s Encrypt, and Google Workspace SMTP relay. Designed for real-world organizational use with HTTPS, DNS, email deliverability, and backup planning.

---

# Executive Summary

## Situation

An organization required a centralized IT helpdesk system that could:

- Accept support requests from any device
- Send confirmation and response emails reliably
- Remain available 24/7
- Use a professional domain name
- Secure user data via HTTPS

Initial state:

- No centralized ticket tracking system
- No structured email response workflow
- No publicly accessible support portal
- No encrypted ticket submission process
- No backup protection for support data

This created operational inefficiencies and potential security risks.

---

## Task

Design and deploy a production-ready IT helpdesk system that:

- Runs continuously on a cloud VPS
- Uses a real domain name
- Enforces HTTPS encryption
- Stores tickets securely in a database
- Sends reliable outbound email
- Protects ticket data with backup procedures
- Remains simple for end users

The solution needed to balance simplicity, security, and reliability.

---

## Action

### Phase 1 – VPS Provisioning & Secure Access

- Provisioned Ubuntu VPS on Vultr
- Created non-root administrative user
- Configured SSH access
- Ensured server reachable publicly

Established a secure, always-on infrastructure foundation.

---

### Phase 2 – Web Stack Deployment (LAMP)

Installed and configured:

- Apache (Web Server)
- PHP with required extensions
- MariaDB (Database)

Validated Apache service:

systemctl status apache2

Created dedicated database:

- helpdesk_db
- helpdesk_user (least privilege)

Applied proper file permissions in `/var/www/helpdesk`.

Configured Apache VirtualHost for dedicated site hosting.

---

### Phase 3 – osTicket Application Installation

- Downloaded osTicket
- Deployed application files to `/var/www/helpdesk`
- Completed web-based installer
- Connected application to MariaDB

Verified successful ticket creation and database storage.

---

### Phase 4 – Domain & DNS Configuration

Configured DNS:

- A record for `helpdesk.empowered901.com`
- Pointed to VPS public IP

Validated propagation across multiple DNS checkers.

Resolved propagation delay issues before SSL provisioning.

---

### Phase 5 – HTTPS & SSL Security

Installed Certbot.

Generated Let’s Encrypt certificate:

sudo certbot --apache -d helpdesk.empowered901.com

Enabled HTTP → HTTPS redirect.

Validated certificate renewal:

sudo certbot renew --dry-run

Ensured encrypted ticket submission and secure login.

---

### Phase 6 – Email & Deliverability Engineering

Configured Google Workspace SMTP relay.

Resolved:

- Blocked SMTP authentication
- SPF conflicts (multiple records issue)
- DNS validation failures

Consolidated SPF record into single valid entry.

Validated DKIM configuration.

Tested:

- Ticket confirmation emails
- Agent reply emails
- End-user response flow

Ensured reliable email communication.

---

### Phase 7 – Backup Strategy Implementation

Planned protection for:

- Database (`helpdesk_db`)
- Application files (`/var/www/helpdesk`)

Created:

mysqldump helpdesk_db > helpdesk_backup.sql

Archived web directory:

tar -czvf helpdesk_files_backup.tar.gz /var/www/helpdesk

Learned correct privilege handling using `sudo -i`.

Stored backups outside web root.

---

## Result

The final system is:

- Publicly accessible via professional domain
- Secured with HTTPS encryption
- Powered by stable LAMP stack
- Using dedicated database user (least privilege)
- Email-enabled with proper SPF/DKIM validation
- Backed up at both database and file level
- Simple and user-friendly for ticket submission
- Production-stable and cloud-hosted

Operational Impact:

- Centralized IT request tracking
- Structured communication workflow
- Reduced email confusion
- Secure handling of user data
- Real-world production service deployment experience

---

## Technologies Used

- Ubuntu Linux (VPS)
- Apache
- PHP
- MariaDB
- osTicket
- Let’s Encrypt (Certbot)
- Google Workspace SMTP Relay
- DNS Management
- Linux CLI tools (mysqldump, tar, systemctl)

---

## Architecture Overview

User → Internet → Apache (HTTPS) → PHP → MariaDB  
Email Flow → osTicket → Google SMTP Relay → User Inbox

Domain:
https://helpdesk.empowered901.com

---

## Skills Demonstrated

- Linux server provisioning
- LAMP stack deployment
- Database configuration & least privilege principles
- DNS configuration & propagation troubleshooting
- SSL certificate automation
- Email deliverability engineering (SPF, DKIM, SMTP relay)
- Backup planning & data protection
- Real-world troubleshooting methodology
- Production service deployment

---

## Future Improvements

- Automated scheduled backups with retention policy
- Off-site backup storage (S3 or equivalent)
- Monitoring & uptime alerts
- Fail2Ban for intrusion protection
- Dockerized deployment for portability
- Configuration automation via Ansible

---

## Project Status

Live & Operational

Public Portal:
https://helpdesk.empowered901.com

Agent Panel:
https://helpdesk.empowered901.com/scp

---

## Author

Terrance Young  
Aspiring DevOps / Systems Engineer
