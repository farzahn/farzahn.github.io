---
title: Cloudflare Tunnels
date: 2023-07-22 14:45:00 -700
categories: [Cloudflare]
tags: [cloudflare,cloudflare_tunnels,ubuntu,reverse_proxy]
---

# What are Cloudflare Tunnels?
Cloudflare(CF) Tunnels are an easy to use reverse proxy solution create by Cloudflare for expose internal services securly to the public internet. The package used to create these tunnels is called cloudflared, and is available for install on many different platforms and Operating Systemss. In this guide, I will be using Ubuntu as my OS and following Cloudflare's documentation for Debian-based x86 64-bit systems.

## My Use Case
I host many services in my homelab, some of which I would like to easily share with friends and family. Cloudflare Tunnels makes this extremly simple by allowing me to define a list of IP Addresses on my local network, which will then use the Cloudflared package to create a secure tunnel out to the Cloudflare and automatically update my Cloudflare DNS records to match. From there I can use Cloudflare Zero Trust to lockdown who has access to which domains. 

Once example of a service I expose to the public internet is Proxmox VE. One of my family members was learning python and wanted to spin-up an Ubuntu VM to use for building and testing their code. Unfortunatly the laptop they had at the time did not provide the nessesary resources to run a VM and support the host. 

To solve for this, I grabbed one of my spare Intel NUCs and installed a fresh instance of Proxmox VE. Then after creating a sperate network and setting up some firewall rules on my Unifi Network (Outside the scope of this documentation), I went ahead and listed the IP Address of the new Proxmox server into Cloudflare Tunnels and viola, Proxmox was now available to them via any old browser. 

Additionally, I wan able to utilize Cloudflare Zero Trust to setup security around the page and only allow users specified in an access group to have access to the server. 

## How to setup Cloudflare Tunnels

### Configure Cloudflare Zero Trust

### Configure Ubuntu Server



