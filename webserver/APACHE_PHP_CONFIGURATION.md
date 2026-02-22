# Apache & PHP Configuration

## Objective

Install and configure Apache and PHP to support the osTicket web application.

---

## Why This Step Matters

- osTicket is a web application.
- It requires a web server to handle HTTP requests.
- It requires PHP to execute application code.
- The server must be able to serve web pages publicly.

---

## Step 1 – Update Package Index

sudo apt update

Purpose:

Ensures the system retrieves the latest available package versions before installation.

---

## Step 2 – Install Apache Web Server

sudo apt install apache2 -y

Purpose:

- Apache handles incoming web requests.
- Serves static and dynamic content.
- Acts as the public-facing web layer.

---

## Step 3 – Install PHP and Required Extensions

Installed PHP and extensions required by osTicket.

Examples include:

- php
- php-mysql
- php-cli
- php-curl
- php-gd
- php-imap
- php-mbstring
- php-xml
- php-zip

Purpose:

These extensions allow osTicket to:

- Connect to the database
- Process forms
- Handle email
- Manage attachments
- Parse XML and other data

---

## Step 4 – Verify Apache Service

systemctl status apache2

Expected result:

active (running)

Also verified by visiting:

http://<server-ip>

Apache default page confirmed successful installation.

---

## Final State

- Apache installed and running
- PHP installed with required extensions
- Server capable of serving web applications
- Environment ready for database configuration
