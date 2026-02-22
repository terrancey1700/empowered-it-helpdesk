# HTTPS Configuration – Let’s Encrypt

## Objective

Secure the helpdesk website using HTTPS encryption to protect user credentials and ticket data.

Domain:

helpdesk.empowered901.com

---

## Why This Step Matters

- Encrypts traffic between users and the server.
- Prevents credential interception.
- Removes browser “Not Secure” warning.
- Required for professional deployment.

---

## Step 1 – Install Certbot

Installed Certbot to manage SSL certificates.

Purpose:

Certbot automates certificate issuance and renewal using Let’s Encrypt.

---

## Step 2 – Request SSL Certificate

Requested certificate for:

helpdesk.empowered901.com

Certbot validated domain ownership and issued certificate.

---

## Step 3 – Enable HTTPS Redirect

Configured automatic redirect from:

http → https

Purpose:

Ensures all traffic uses encrypted connection.

---

## Step 4 – Verify Certificate Renewal

Confirmed certificate renewal process works properly.

Purpose:

Let’s Encrypt certificates expire every 90 days.
Automatic renewal ensures continuous HTTPS protection.

---

## Issue Encountered

Certificate request initially failed.

Root Cause:

DNS propagation delay prevented domain validation.

Resolution:

Waited for DNS propagation before retrying.

---

## Final State

- HTTPS active on helpdesk domain
- HTTP traffic automatically redirected
- Certificate renewal confirmed
- Encrypted communication enforced
