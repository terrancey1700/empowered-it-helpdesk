# osTicket Deployment

## Objective

Deploy the osTicket application and configure Apache to serve it from a dedicated web directory.

---

## Why This Step Matters

- osTicket must be placed in the correct web directory.
- Apache must know where to load the application from.
- Proper permissions are required for the web server to access files.

---

## Step 1 – Download osTicket

Downloaded the osTicket package from the official source.

Extracted the archive.

---

## Step 2 – Move Application Files

Copied the contents of the `upload/` directory into:

/var/www/helpdesk

Purpose:

This directory becomes the root directory for the helpdesk site.

---

## Step 3 – Set File Permissions

Adjusted file permissions so Apache can read and serve the application files.

Purpose:

- Prevent permission denied errors
- Allow proper web server access
- Ensure installer can write configuration files

---

## Step 4 – Create Apache VirtualHost

Created a site configuration file in:

/etc/apache2/sites-available/

Configured VirtualHost to point to:

/var/www/helpdesk

Purpose:

- Allows Apache to serve the helpdesk from its own site configuration
- Supports domain-based hosting

---

## Step 5 – Enable Site

Enabled the new site configuration.

Reloaded Apache to apply changes.

Purpose:

Activates the helpdesk site configuration.

---

## Step 6 – Complete Web Installer

Visited the helpdesk URL in a browser.

Completed the osTicket web-based installation process:

- Entered database name
- Entered database user
- Entered database password
- Created admin account

Confirmed successful installation.

---

## Final State

- osTicket installed in /var/www/helpdesk
- Apache serving the application
- Database connected successfully
- Admin panel accessible
- Public helpdesk portal operational
