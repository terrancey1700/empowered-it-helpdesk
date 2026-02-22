# Troubleshooting – Common Issues & Resolutions

This document outlines real problems encountered during deployment and how they were resolved.

Each issue includes:

- Issue
- Root Cause
- Resolution
- Lesson Learned

---

## 1. DNS Propagation Delay

### Issue

The domain loaded locally but Certbot failed validation.

### Root Cause

DNS changes had not fully propagated across the internet.

Let’s Encrypt could not verify domain ownership.

### Resolution

- Waited for DNS propagation.
- Verified domain resolution from multiple sources.
- Retried Certbot after confirmation.

### Lesson Learned

DNS changes are not instant.

Always verify global DNS resolution before requesting SSL certificates.

---

## 2. Google Workspace Blocking SMTP Authentication

### Issue

Outbound email failed using standard username/password SMTP authentication.

### Root Cause

Google Workspace security policies restricted basic authentication.

### Resolution

Configured SMTP relay to trust the VPS public IP instead of using basic authentication.

### Lesson Learned

Cloud email providers enforce strict security policies.

SMTP relay tied to server IP is often more reliable than basic authentication.

---

## 3. SPF Record Conflict

### Issue

Emails failed SPF validation.

### Root Cause

Multiple SPF records existed for the domain.

Domains must have exactly one SPF record.

### Resolution

Merged all senders into a single valid SPF record.

Example structure:

v=spf1 include:_spf.google.com ip4:<server-ip> ~all

### Lesson Learned

SPF records must be consolidated into one entry.
Multiple SPF records invalidate email authentication.

---

## 4. Linux Permission Errors

### Issue

Received "Permission denied" when creating backups.

### Root Cause

Attempted to write to restricted directories without proper privileges.

### Resolution

Used:

sudo -i

to operate with root privileges when required.

### Lesson Learned

Always confirm user context before running administrative commands.

---

## 5. Running Server Commands Locally

### Issue

Attempted to run commands like systemctl on local machine instead of the VPS.

### Root Cause

Lost track of whether the active terminal session was local or remote.

### Resolution

Verified SSH session before executing server commands.

### Lesson Learned

Always confirm environment context (local vs remote server) before running system-level commands.

---

## Final Outcome

All major deployment issues were resolved using structured troubleshooting:

1. Identify the layer (DNS, SSL, Email, Permissions)
2. Isolate the root cause
3. Apply targeted fix
4. Retest before proceeding

The system is now stable, secure, and operational.
