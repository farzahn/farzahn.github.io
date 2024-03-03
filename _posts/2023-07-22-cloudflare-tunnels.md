---
title: Cloudflare Tunnels
date: 2023-07-22 14:45:00 -700
categories: [Cloudflare]
tags: [cloudflare,cloudflare_tunnels,ubuntu,reverse_proxy]
---

# What are Cloudflare Tunnels?

Cloudflare (CF) Tunnels are an easy-to-use reverse proxy solution created by Cloudflare to securely expose internal services to the public internet. The package used to create these tunnels is called "cloudflared," and it is available for installation on various platforms and operating systems. In this guide, I will be using Ubuntu as my OS and following Cloudflare's documentation for Debian-based x86 64-bit systems.

## My Use Case

I host many services in my homelab, some of which I would like to easily share with friends and family. Cloudflare Tunnels make this extremely simple by allowing me to define a list of IP addresses on my local network. These addresses will then use the "cloudflared" package to create a secure tunnel out to Cloudflare and automatically update my Cloudflare DNS records to match. From there, I can use Cloudflare Zero Trust to lock down who has access to which domains.

An example of a service I expose to the public internet is Proxmox VE. One of my family members was learning Python and wanted to spin up an Ubuntu VM to use for building and testing their code. Unfortunately, the laptop they had at the time did not provide the necessary resources to run a VM and support the host.

To solve this issue, I grabbed one of my spare Intel NUCs and installed a fresh instance of Proxmox VE. After creating a separate network and setting up some firewall rules on my Unifi Network (outside the scope of this documentation), I listed the IP address of the new Proxmox server into Cloudflare Tunnels, and voila, Proxmox was now available to them via any browser.

Additionally, I was able to utilize Cloudflare Zero Trust to set up security around the page and only allow users specified in an access group to have access to the server.

## How to Set up Cloudflare Tunnels

### Configure Cloudflare Zero Trust

### Configure Ubuntu Server




