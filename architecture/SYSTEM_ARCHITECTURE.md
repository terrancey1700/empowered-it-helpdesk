# System Architecture – Empowered IT Helpdesk

## Overview

This project deploys osTicket on a cloud-hosted Ubuntu VPS using a traditional LAMP stack.

The system is publicly accessible via a custom domain and secured with HTTPS.

---

## High-Level Architecture

User  
↓  
Internet  
↓  
Apache (HTTPS)  
↓  
PHP Runtime  
↓  
MariaDB Database  

Email Flow:

osTicket → Google Workspace SMTP Relay → User Inbox

---

## Infrastructure Components

- Cloud Provider: Vultr VPS
- Operating System: Ubuntu Linux
- Web Server: Apache
- Application Runtime: PHP
- Database: MariaDB
- SSL: Let’s Encrypt (Certbot)
- Email: Google Workspace SMTP Relay
- DNS: A record pointing to VPS IP

---

## Design Decisions

### Why VPS Instead of Local VM?

- 24/7 availability
- Public accessibility
- Real-world deployment experience
- Independent from local hardware

### Why Apache?

- Stable and widely supported
- Compatible with osTicket
- Easy VirtualHost configuration

### Why Dedicated Database User?

- Principle of least privilege
- Reduces risk if application is compromised

### Why HTTPS?

- Encrypts credentials and ticket data
- Prevents browser security warnings
- Required for professional deployment

---

## Security Boundaries

- Only port 80 and 443 exposed publicly
- SSH access restricted to administrator
- Database bound to localhost
- Dedicated database user with limited privileges

---

## Final State

The system operates as a production-ready web application with:

- Secure HTTPS access
- Functional email communication
- Dedicated database
- Structured backup process
