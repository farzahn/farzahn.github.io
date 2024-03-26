---
title: Proxmox Authentication with Google OAuth
date: 2024-35-03 17:30:00 -700
categories: [Proxmox]
tags: [proxmox,server,oidc,oauth,google,auth,authentication]
---

# Using Google Auth with Proxmox

## In Google Cloud Console:

### For Creating Credentials
1. Head to [Google Cloud Console](https://console.cloud.google.com/) and log in with the account you want to use for Google Auth.
2. In the pulldown at the top to the right of "Google Cloud," select an existing project or create a new one (e.g., "Proxmox Auth").
3. Select "API & Services" from Quick Access or the sandwich menu on the upper left.
4. Select "Credentials" and click "+ Create Credentials" and select "OAuth Client ID".
5. For application type, select "Web Application" and give it a helpful name.
6. For Authorized Javascript Origins, enter your full hostname with FQDN for Proxmox, e.g., `https://proxmox.domain.com`.
7. For Authorized redirect URIs, enter the page you actually access for Proxmox with port, e.g., `https://proxmox.domain.com:8006`.
8. Save.

### For OAuth Consent Screen
- If at any point above you're asked to create a consent screen, go ahead and click "Configure Consent Screen".
- Select the type of access. Internal means restricted to the workspace domain you're currently using.
- Add an app name, pick an existing email for support, add a logo if you want.
- Add your host+FQDN as above (e.g., `https://proxmox.domain.com`) to App Domain.
- Add your Authorized Domains.
- Add a developer email and click "Save and Continue".

### For Scopes
- Click Add or Remove Scopes.
- Add scopes to "Non-sensitive scopes".
- Review the summary and click "Back to Dashboard".

## In Proxmox

### Initial Setup for Auth
1. Click on Datacenter in the tree.
2. Scroll down to Permissions, expand that subtree, and click Realms.
3. Click "Add" and select OpenID Connect Server.
4. Add the Issuer URL of `https://accounts.google.com`.
5. In the "Realm:" field, add something like "GoogleAuth".
6. Paste the Client ID and Client Key from the Google credentials page.
7. Do not check "autocreate users".
8. Select Username Claim of "email".
9. For Scopes enter "email profile openid" (leaving spaces between scopes).
10. For Prompt select "login".
11. Select if you want this realm to be default and enter a useful comment. Leave ACR Values blank.
12. Click Add.

### Adding Users in Proxmox
1. Under the permissions subtree, select Users.
2. Click Add.
3. For the User Name enter the workspace account email address.
4. Add the user to any groups and add any metadata you like here.
5. Proxmox will append "@<realmname>" to the username.
6. Click Add.