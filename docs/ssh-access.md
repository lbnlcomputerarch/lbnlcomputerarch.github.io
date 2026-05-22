---
layout: page
title: SSH Access
permalink: /docs/ssh-access/
---

## SSH Access

This guide covers how to connect to CAG computing resources using SSH.

## Prerequisites

- An active CAG account on a specific server
- SSH installed on your local machine (pre-installed on macOS and most Linux distributions)

## Basic Connection

To connect to one of our servers via SSH, run:

```ssh
ssh USERNAME@SERVER.HOSTNAME.lbl.gov
```

Replace `USERNAME` with your CAG username and `SERVER.HOSTNAME.lbl.gov` with the target server address.

You will be prompted for your CAG password.

## SSH Key Setup (Recommended)

Using SSH keys is more secure and convenient than entering your password each time.

### 1. Generate an SSH key pair

On your local machine:

```bash
ssh-keygen -t ed25519 -C "you@lbl.gov"
```

Press Enter to accept the default location, or specify a custom path. When asked for a passphrase, you may leave it empty (not recommended) or set a strong one.

### 2. Copy the public key to the server

```bash
ssh-copy-id USERNAME@SERVER.HOSTNAME.lbl.gov
```

If `ssh-copy-id` is not available on your system:

```bash
cat ~/.ssh/id_ed25519.pub | ssh USERNAME@SERVER.HOSTNAME.lbl.gov "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

### 3. Test the connection

```bash
ssh USERNAME@SERVER.HOSTNAME.lbl.gov
```

You should connect without a password prompt.

## SSH Configuration

You can simplify connections by creating or editing your local `~/.ssh/config` file:

```
Host cag-server
    HostName SERVER.HOSTNAME.lbl.gov
    User USERNAME
    Port 22
    IdentityFile ~/.ssh/id_ed25519
    ForwardAgent true
```

Then you can simply run:

```bash
ssh cag-server
```

### Configuration options

| Option | Description |
|--------|-------------|
| `Host` | Alias for the server (what you type to connect) |
| `HostName` | Actual server address |
| `User` | Your CAG username |
| `Port` | SSH port (default: 22) |
| `IdentityFile` | Path to your private key |
| `ForwardAgent` | Enables SSH agent forwarding for jump hosts |

## SSH Agent Forwarding

If you need to connect from one of our servers to external systems, enable agent forwarding:

```bash
ssh -A USERNAME@SERVER.HOSTNAME.lbl.gov
```

On your local machine, make sure you have an SSH agent running with your key loaded:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

## Troubleshooting

| Problem | Possible cause | Solution |
|---------|---------------|----------|
| Connection refused | Server is down or wrong address | Verify `SERVER.HOSTNAME.lbl.gov` and try again |
| Permission denied (publickey) | Key not added or wrong key | Run `ssh-copy-id` or check `~/.ssh/authorized_keys` |
| Connection timed out | Firewall or network issue | Confirm you are on LBNL network or using VPN |
| Too many authentication failures | No keys offered | Use `-i ~/.ssh/id_ed25519` or configure `~/.ssh/config` |
