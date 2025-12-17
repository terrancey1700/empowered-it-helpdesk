# empowered-it-helpdesk
# Project Summary: Empowered IT Helpdesk (osTicket)

This project is a real IT helpdesk system built for a school or organization. It lets people report IT problems (like Wi-Fi issues, device issues, account problems, or classroom tech problems) by submitting a ticket. 

The helpdesk is hosted online, secured with HTTPS, and connected to a real domain name. It is designed to stay simple so users can write what is wrong without getting stuck choosing complicated categories.

---

## What This Project Does

* Provides a public website where users can submit IT support tickets.
* Lets the administrator (me) respond to users by email.
* Tracks every request and every reply in one place.
* Runs on a cloud server so it can be reached from any device.

---

## Steps Completed (With Why, How, and What to Do)

### Step 1: Choose Where to Host the Helpdesk

Why this step matters:

* A helpdesk needs to be available anytime. If it runs only on a local computer or a VM that is turned off, users cannot reach it.
* A cloud server stays online even when your laptop is off.

How it was done:

* I created a VPS (virtual private server) on Vultr.
* I used Ubuntu Linux as the operating system.

What to do to complete this step:

* Create a VPS.
* Log in to the server using SSH.
* Create a normal admin user and give it sudo access (so you do not work as root all the time).

---

### Step 2: Install the Web Server and Required Software

Why this step matters:

* osTicket is a web application, so it needs a web server.
* It also needs PHP to run the app code.
* It needs a database to store tickets, users, and settings.

How it was done:

* Installed Apache (web server).
* Installed PHP and required PHP extensions.
* Installed MariaDB (MySQL-compatible database).

What to do to complete this step:

* Update the server packages.
* Install Apache.
* Install PHP and common extensions used by osTicket.
* Install MariaDB.
* Confirm Apache is running and serving pages.

---

### Step 3: Configure the Database for osTicket

Why this step matters:

* osTicket needs a database to store tickets, messages, users, and configuration.
* Using a dedicated database and user is safer and cleaner than using the database root account.

How it was done:

* Created a database named `helpdesk_db`.
* Created a database user (example: `helpdesk_user`).
* Granted that user permission to access only the helpdesk database.

What to do to complete this step:

* Log into MariaDB.
* Create the database.
* Create the database user.
* Grant privileges.
* Save the username and password for the osTicket installer.

---

### Step 4: Install osTicket and Configure Apache

Why this step matters:

* osTicket files must be placed in the correct web folder.
* Apache needs a site configuration so the helpdesk loads from the right location.

How it was done:

* Downloaded osTicket.
* Copied the `upload/` folder contents into a web folder (example: `/var/www/helpdesk`).
* Set correct file permissions so Apache can read the files.
* Created an Apache VirtualHost configuration for the helpdesk.

What to do to complete this step:

* Place osTicket in `/var/www/helpdesk`.
* Create a site config file in `/etc/apache2/sites-available/`.
* Enable the site and reload Apache.
* Visit the helpdesk URL and complete the osTicket web installer.

---

### Step 5: Connect a Real Domain Name

Why this step matters:

* A domain name is easier to remember than an IP address.
* A real domain looks professional and is easier to share.

How it was done:

* Created a DNS record for `helpdesk.empowered901.com` pointing to the server IP.

What to do to complete this step:

* In your domain DNS settings, add an A record:

  * Host: helpdesk
  * Points to: your server IP
* Wait for DNS to propagate

---

### Step 6: Enable HTTPS (Secure Website)

Why this step matters:

* HTTPS encrypts traffic so passwords and ticket details are protected.
* Browsers warn users when a site is not secure.

How it was done:

* Used Let’s Encrypt and Certbot to create and renew certificates.
* Confirmed certificate renewal works.

What to do to complete this step:

* Install Certbot.
* Request a certificate for helpdesk domain.
* Enable automatic redirect from HTTP to HTTPS.
* Confirm renewal works.

---

### Step 7: Simplify Help Topics and Add a Custom Field

Why this step matters:

* Too many categories confuse users.
* A simple intake form makes it more likely people will submit tickets.
* The organization/school field helps support understand where the problem is coming from.

How it was done:

* Reduced help topics to keep the user experience simple.
* Added a required custom field named “Organization / School” in the Ticket Details form.

What to do to complete this step:

* In osTicket Admin Panel:

  * Keep one main help topic for IT requests.
  * Add a new form field (short answer) labeled “Organization / School”.
  * Make the field required.

---

### Step 8: Configure Outgoing Email (SMTP) and Deliverability

Why this step matters:

* Users expect confirmation emails.
* Users expect email replies.
* PHP mail is often unreliable on cloud servers.
* SPF and DKIM prevent emails from being flagged as spam.

How it was done:

* Configured Google Workspace for outgoing email.
* Set up SMTP relay rules to allow the server to send mail.
* Fixed SPF by merging multiple SPF records into one valid SPF record.

What to do to complete this step:

* Configure outbound SMTP in osTicket.
* If using Google Workspace:

  * Configure SMTP relay to trust your server IP.
* Verify DNS:

  * Make sure only one SPF record exists.
  * Make sure DKIM records are present.
* Test ticket submission and email replies.

---

### Step 9: Create Backups (Database and Files)

Why this step matters:

* If the server breaks or is breached, backups protect the ticket history.
* The database contains the ticket data.
* The web folder contains configuration and attachments.

How it was done:

* Planned backups for:

  * Database (`helpdesk_db`)
  * Application files (`/var/www/helpdesk`)
* Learned that backups must be run with correct permissions (root or sudo).

What to do to complete this step:

* Become root using `sudo -i`.
* Create a database dump.
* Create a compressed archive of the helpdesk folder.
* Store backups outside the web directory.

---

## Pain Points and Struggles

These are the main areas where I struggled, and what I learned:

1. DNS propagation delays

* The domain would load for me, but Certbot failed because Let’s Encrypt could not see the DNS record yet.
* Lesson learned: DNS changes can take time across the internet. Always verify DNS from multiple locations.

2. SMTP and Google Workspace security

* Google blocked standard username/password SMTP and required application-specific authentication.
* App Passwords were not available due to Workspace settings.
* Lesson learned: Google Workspace email is secure by default and often requires SMTP relay or admin policy changes.

3. SPF record conflicts

* I had multiple SPF records, which breaks SPF validation.
* Lesson learned: a domain must have one SPF record, and it must include all allowed senders.

4. Linux permissions

* I tried saving backups inside `/root` as a non-root user and got permission denied errors.
* Lesson learned: `/root` is private. Use `sudo -i` or store backups in a directory owned by your user.

5. Server access and command context

* I ran commands locally on my Mac that only work on the server (like systemctl).
* Lesson learned: always confirm whether you are on your laptop or on the Linux server before running commands.

---

## What I Would Improve Next

* Automated daily backups with retention (keep last 7 to 14 days)
* Off-server backup storage (S3 or another storage provider)
* Clean email templates and consistent ticket subject formatting
* Optional incoming email ticket creation (IMAP) if the organization wants email-only ticket creation

---

## Project Status

The helpdesk is live, secured with HTTPS, and configured for simple ticket intake and support responses.

* Public portal: [https://helpdesk.empowered901.com](https://helpdesk.empowered901.com)
* Agent panel: [https://helpdesk.empowered901.com/scp](https://helpdesk.empowered901.com/scp)
