---
title: Cloudflare Tunnels
date: 2023-07-22 14:45:00 -700
categories: [Cloudflare]
tags: [cloudflare,cloudflare_tunnels,ubuntu,reverse_proxy]
---

# Setting Up Cloudflare Tunnels on Ubuntu Server

## What are Cloudflare Tunnels?

Cloudflare Tunnels provide a user-friendly reverse proxy solution designed by Cloudflare to securely expose internal services to the public internet. The primary tool for creating these tunnels is called "cloudflared," which can be installed on various platforms. In this guide, we'll focus on Ubuntu Server, a Debian-based system.

## My Use Case

I manage multiple services in my homelab and wish to easily share them with friends and family. Cloudflare Tunnels simplify this process by enabling the creation of secure connections for specified local IP addresses. These connections utilize the "cloudflared" package to establish tunnels to Cloudflare, automatically updating DNS records. Cloudflare Zero Trust can then be employed to control access to specific domains.

For instance, I expose services like Proxmox VE to the public internet. A family member, engaged in Python learning, needed an Ubuntu VM for code development. Using Cloudflare Tunnels, I connected the VM securely, making it accessible through any browser. Cloudflare Zero Trust allowed me to enforce access restrictions, enhancing security.

## How to Set up Cloudflare Tunnels on Ubuntu Server

### Install Cloudflare Tunnel on Ubuntu Server

1. **Install Cloudflared**: Begin by downloading and installing the `cloudflared` daemon on your Ubuntu Server. Use the appropriate package manager or follow Cloudflare's documentation for Ubuntu.

    ```bash
    sudo apt-get update
    sudo apt-get install cloudflared
    ```

2. **Authenticate the Cloudflare Tunnel daemon**: After installation, authenticate the daemon with your Cloudflare account by executing the command:

    ```bash
    cloudflared login
    ```

    This will open a browser window, allowing you to log in and authorize the daemon.

3. **Create a Tunnel**: Once authenticated, create a tunnel by executing:

    ```bash
    cloudflared tunnel create <TUNNEL-NAME>
    ```

    Replace `<TUNNEL-NAME>` with your preferred name. This command generates a new tunnel with the specified name and necessary credentials.

### Configure Cloudflare Zero Trust

1. **Configure Zero Trust policies**: In the Cloudflare dashboard, go to the `Access` tab and create a new Zero Trust policy. Specify the hostname of the tunnel you created earlier and configure the policy to allow or deny access based on your requirements.

    - Click on the "Access" tab in the Cloudflare dashboard.
    - Navigate to the "Policies" section and click "Create a Policy."
    - Choose "Zero Trust" as the policy type.
    - Specify the hostname associated with your tunnel.
    - Define rules to allow or deny access based on user groups, IP ranges, or other criteria.

2. **Assign Users to Access Groups**: In the Cloudflare dashboard, under the "Access" tab, manage user access by creating access groups. Assign users to these groups based on your organization's structure.

3. **Test Access Policies**: Before running the tunnel, verify the Zero Trust policies. Attempt to access the services associated with your tunnel from different devices and users, ensuring the policies are correctly applied.

### Run the Tunnel

1. **Start the Tunnel**: After configuring Zero Trust policies, start the tunnel by executing:

    ```bash
    cloudflared tunnel run <TUNNEL-NAME>
    ```

    This command establishes a secure connection between your infrastructure and Cloudflare's edge network, enforcing the Zero Trust policies configured earlier.

2. **Monitor and Adjust**: Monitor the tunnel's performance and adjust Zero Trust policies as needed. Cloudflare's dashboard provides real-time insights into traffic and access attempts.

These steps provide a comprehensive setup for Cloudflare Tunnels on Ubuntu Server, including additional guidance on configuring Cloudflare Zero Trust for enhanced security. Further customization can be done with Zero Trust policies and tunnel settings to match your specific needs.
