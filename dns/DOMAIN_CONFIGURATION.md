# Domain & DNS Configuration

## Objective

Connect the helpdesk application to a real domain name for public access.

Domain:

helpdesk.empowered901.com

---

## Why This Step Matters

- Domain names are easier to remember than IP addresses.
- A custom domain looks professional.
- Required for HTTPS certificate issuance.

---

## Step 1 – Create DNS A Record

In domain DNS settings:

Type: A  
Host: helpdesk  
Points to: <VPS Public IP>

Purpose:

Maps the domain to the server hosting the application.

---

## Step 2 – Wait for DNS Propagation

After creating the A record:

- DNS changes required time to propagate.
- The domain did not immediately resolve everywhere.

---

## Issue Encountered

Certbot failed initially because Let’s Encrypt could not verify the domain.

Root Cause:

DNS propagation delay.

Resolution:

Waited for DNS propagation and verified domain resolution before retrying certificate request.

---

## Lesson Learned

- DNS updates are not instant.
- Always confirm DNS resolution from multiple locations before requesting SSL certificates.

---

## Final State

- helpdesk.empowered901.com resolves to VPS IP
- Domain accessible publicly
- Ready for HTTPS configuration
