---
title: How to Mount an SMB Share
date: 2024-04-07 12:47:00 -700
categories: [Truenas]
tags: [ubuntu,proxmox,smb,mount,storage]
---

# How to Mount an SMB Share to Ubuntu Server

Mounting an SMB share to an Ubuntu Server allows you to access files and directories stored on a remote Windows or Samba server. This can be particularly useful for sharing files across a network. Here's how to do it:

## Step 1: Install cifs-utils

First, ensure that `cifs-utils` is installed on your Ubuntu Server. If not, you can install it using the following command:

```bash
sudo apt-get install cifs-utils
```

## Step 2: Create a .smbcredentials File

You should create a `.smbcredentials` file to securely store the username and password required to access the SMB share. This helps to avoid storing sensitive information directly in your scripts or configuration files.

```bash
sudo nano /etc/smbcredentials
```

Add the following lines to the file, replacing `username` and `password` with your credentials:

```
username=your_username
password=your_password
```

Save the file and exit the text editor.

Make sure the `.smbcredentials` file has restricted permissions to maintain security:

```bash
sudo chmod 600 /etc/smbcredentials
```

## Step 3: Mount the SMB Share

Now, you can proceed to mount the SMB share. You can either mount it manually or add an entry to `/etc/fstab` for automatic mounting during system boot.

### Manual Mounting

Use the following command to manually mount the SMB share:

```bash
sudo mount -t cifs //server/share /mnt/point -o credentials=/etc/smbcredentials,uid=1000,gid=1000
```

Replace `//server/share` with the path to your SMB share and `/mnt/point` with the local directory where you want to mount the share.

### Automatic Mounting with /etc/fstab

To automatically mount the SMB share during system boot, edit the `/etc/fstab` file:

```bash
sudo nano /etc/fstab
```

Add a new line at the end of the file with the following format:

```
//server/share /mnt/point cifs credentials=/etc/smbcredentials,uid=1000,gid=1000 0 0
```

Replace `//server/share` with the path to your SMB share, `/mnt/point` with the local directory, and `uid=1000,gid=1000` with your user's UID and GID (use `id` command to find them).

Save the file and exit the text editor.

## Step 4: Test the Mount

Finally, test the mount by accessing the mounted directory:

```bash
ls /mnt/point
```

If everything is configured correctly, you should see the files and directories from the SMB share listed in the output.

## Step 5: Mount All Filesystems

If you've added the entry to `/etc/fstab`, you can mount all filesystems mentioned in this file by running:

```bash
sudo mount -a
```

This command will mount all entries in `/etc/fstab` that have the `auto` option set. It's particularly useful for testing if your newly added SMB share entry is correctly configured in `/etc/fstab`.

## Adding SMB Share in Proxmox

If you're using Proxmox, you can add an SMB share as a storage option. Here's how:

1. Log in to the Proxmox web interface.

2. Navigate to "Datacenter" in the left sidebar.

3. Click on "Storage" in the top menu.

4. Click the "Add" button.

5. Choose "CIFS" from the dropdown menu.

6. Fill in the required information:
   - ID: A unique identifier for the storage (e.g., `smb_storage`).
   - Server: The IP address or hostname of the SMB server.
   - Share: The name of the shared folder.
   - Username: Your username for accessing the SMB share.
   - Password: Your password for accessing the SMB share.

7. Click "Add" to save the configuration.

8. Once added, you can use this SMB share as storage for your Proxmox virtual machines or containers.

That's it! You have successfully mounted an SMB share to your Ubuntu Server and added an SMB share as storage in Proxmox. You can now access and use the shared files and directories as needed.
