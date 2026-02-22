# VPS Provisioning – Ubuntu Server Setup

## Objective

Provision a cloud-hosted Ubuntu VPS to deploy the osTicket helpdesk application.

---

## Step 1 – Create VPS

Cloud Provider: Vultr

Configuration:

- Operating System: Ubuntu Linux
- Public IPv4 address assigned

Purpose:

A VPS ensures:

- 24/7 availability
- Public accessibility
- Independence from local hardware

---

## Step 2 – Initial SSH Access

Connected to the server using SSH:

ssh root@<server-ip>

Confirmed successful login.

---

## Step 3 – Create Non-Root Administrative User

Created a standard user account.

Granted sudo privileges so administrative tasks can be performed without operating as root.

Purpose:

- Avoid daily use of root account
- Follow basic Linux administration best practice

---

## Final State

- VPS provisioned
- Ubuntu installed
- SSH access confirmed
- Non-root administrative user created
- Server ready for web server installation
