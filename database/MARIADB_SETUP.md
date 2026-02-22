# MariaDB Setup for osTicket

## Objective

Create a dedicated database and database user for the osTicket application.

---

## Why This Step Matters

- osTicket stores tickets, messages, users, and settings in a database.
- Using a dedicated database user is safer than using the root account.
- Limits database access to only what the application needs.

---

## Step 1 – Access MariaDB

Log into MariaDB:

sudo mysql

This opens the MariaDB command-line interface.

---

## Step 2 – Create Database

CREATE DATABASE helpdesk_db;

Purpose:

Creates a dedicated database for the helpdesk system.

---

## Step 3 – Create Database User

CREATE USER 'helpdesk_user'@'localhost' IDENTIFIED BY 'secure_password';

Purpose:

Creates a user that will only be used by osTicket.

---

## Step 4 – Grant Privileges

GRANT ALL PRIVILEGES ON helpdesk_db.* TO 'helpdesk_user'@'localhost';

FLUSH PRIVILEGES;

Purpose:

- Allows the helpdesk user to access only the helpdesk database.
- Prevents access to other databases on the server.

---

## Step 5 – Save Credentials

The database name, username, and password were saved for use during the osTicket web installer.

---

## Final State

- Database `helpdesk_db` created
- User `helpdesk_user` created
- Privileges limited to helpdesk database
- Database ready for osTicket installation
