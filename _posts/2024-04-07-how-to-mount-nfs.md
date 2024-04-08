---
title: How to Mount an NFS Share
date: 2024-04-07 12:47:00 -700
categories: [Truenas]
tags: [ubuntu,proxmox,nfs,mount,storage]
---

# How to Mount an NFS Share to Ubuntu Server

Mounting an NFS share to an Ubuntu Server allows you to access files and directories stored on a remote NFS server. NFS (Network File System) is a distributed file system protocol. Here's how to mount an NFS share:

## Step 1: Install NFS Client Utilities

First, ensure that NFS client utilities are installed on your Ubuntu Server. If not, you can install them using the following command:

```bash
sudo apt-get install nfs-common
```

## Step 2: Mount the NFS Share

Now, you can proceed to mount the NFS share. You can either mount it manually or add an entry to `/etc/fstab` for automatic mounting during system boot.

### Manual Mounting

Use the following command to manually mount the NFS share:

```bash
sudo mount -t nfs server:/path/to/share /mnt/point
```

Replace `server:/path/to/share` with the server IP or hostname and the path to the NFS share. Also, replace `/mnt/point` with the local directory where you want to mount the share.

### Automatic Mounting with /etc/fstab

To automatically mount the NFS share during system boot, edit the `/etc/fstab` file:

```bash
sudo nano /etc/fstab
```

Add a new line at the end of the file with the following format:

```
server:/path/to/share /mnt/point nfs defaults 0 0
```

Replace `server:/path/to/share` with the server IP or hostname and the path to the NFS share, and `/mnt/point` with the local directory where you want to mount the share.

Save the file and exit the text editor.

## Step 3: Test the Mount

Finally, test the mount by accessing the mounted directory:

```bash
ls /mnt/point
```

If everything is configured correctly, you should see the files and directories from the NFS share listed in the output.

## Step 4: Mount All Filesystems

If you've added the entry to `/etc/fstab`, you can mount all filesystems mentioned in this file by running:

```bash
sudo mount -a
```

This command will mount all entries in `/etc/fstab` that have the `auto` option set. It's particularly useful for testing if your newly added NFS share entry is correctly configured in `/etc/fstab`.

That's it! You have successfully mounted an NFS share to your Ubuntu Server. You can now access the files and directories as needed.
