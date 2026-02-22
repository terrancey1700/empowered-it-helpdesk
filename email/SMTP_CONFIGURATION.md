# SMTP & Email Deliverability Configuration

## Objective

Enable reliable outbound email for ticket confirmations and agent replies.

The helpdesk must:

- Send confirmation emails when a ticket is submitted.
- Send replies when agents respond.
- Avoid being flagged as spam.

---

## Why This Step Matters

- PHP mail is often unreliable on cloud servers.
- Modern email providers require proper authentication.
- SPF and DKIM are necessary for email deliverability.

---

## Email Provider

Google Workspace (SMTP Relay)

Used SMTP relay instead of basic username/password authentication.

---

## Step 1 – Configure SMTP in osTicket

In osTicket Admin Panel:

- Configured outbound SMTP settings.
- Entered Google SMTP relay details.
- Used server IP authorization for relay.

Purpose:

Allows the VPS to send mail through Google’s mail servers.

---

## Step 2 – Configure Google Workspace SMTP Relay

In Google Admin Console:

- Created SMTP relay rule.
- Allowed mail from the VPS public IP.
- Ensured relay accepts connections from the server.

Purpose:

Prevents authentication blocks and improves reliability.

---

## Step 3 – Fix SPF Record

Issue:

Multiple SPF records existed for the domain.

Problem:

A domain must have only one SPF record.
Multiple records invalidate SPF checks.

Resolution:

Merged all allowed senders into a single valid SPF record.

Example structure:

v=spf1 include:_spf.google.com ip4:<server-ip> ~all

---

## Step 4 – Verify DKIM

Confirmed DKIM was properly configured in DNS.

Purpose:

- Improves email trust.
- Prevents spoofing.
- Reduces spam filtering.

---

## Testing

Submitted test tickets.

Verified:

- Confirmation email delivered.
- Agent replies delivered.
- Emails not marked as spam.

---

## Issues Encountered

### Google Blocking SMTP Authentication

Standard username/password SMTP was restricted.

Resolution:

Used SMTP relay configuration tied to server IP.

---

### SPF Record Conflict

Multiple SPF records caused validation failure.

Resolution:

Consolidated into one valid SPF record.

---

## Final State

- Outbound email functional
- SPF valid
- DKIM active
- Ticket confirmation and reply workflow working
- Email deliverability stabilized
