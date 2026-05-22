---
layout: page
title: XRDP Remote GUI
permalink: /docs/xrdp-tunnel/
---

## XRDP Remote GUI

This guide covers how to access a remote graphical desktop on our servers using XRDP through an SSH tunnel. SSH tunneling encrypts the VNC traffic so you can connect securely, even from untrusted networks.

## Prerequisites

- SSH access to our servers (see [SSH Access]({{ site.baseurl }}/docs/ssh-access/))
- A desktop environment already installed on the server (see below if you need to install one)
- An XRDP client (remote desktop viewer) on your local machine
    - **macOS**: [Microsoft Remote Desktop](https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466) (free)
    - **Windows**: [Microsoft Remote Desktop](https://apps.microsoft.com/detail/9wzdncrfj3t6) (built in as "Remote Desktop Connection")
    - **Linux**: `remmina` or `rdesktop`

## Step 1 — Create an SSH Tunnel

From your local machine, open an SSH tunnel that forwards a local port to the server's XRDP port:

```bash
ssh -L 33890:localhost:3389 USERNAME@SERVER.HOSTNAME.lbl.gov
```

- The `-L` flag creates a local port forward
- `33890` is the local port you will connect to
- `3389` is XRDP's port on the remote server
- This tunnel must stay open while you are using the remote desktop
- **Keep this terminal window open** — closing it closes the tunnel

You can also add this to your `~/.ssh/config`:

```
Host cag-desktop
    HostName SERVER.HOSTNAME.lbl.gov
    User USERNAME
    LocalForward 33890 localhost:3389
    IdentityFile ~/.ssh/id_ed25519
```

Then:

```bash
ssh cag-desktop
```

## Step 2 — Connect with Your Remote Desktop Client

Open your remote desktop application and connect to:

```
localhost:33890
```

When prompted:

1. Enter your LBNL username
2. Enter your LBNL password
3. Choose a session type (VNC or Xorg — Xorg is recommended)
4. Click Connect

You should see a graphical desktop session.

## Troubleshooting

| Problem | Possible cause | Solution |
|---------|---------------|----------|
| XRDP won't start | X11 lock file conflict | Run `sudo rm /tmp/.X11-lock /tmp/.X0-lock` then restart xrdp |
| Black screen after login | Desktop environment not set | Add `gnome-session` or `xfce4-session` to `~/.xsession` |
| Tunnel won't connect | Firewall blocking | Ensure local port 33890 is not blocked; try a different port |
| Mouse not working | XRDP session type | Try switching from VNC to Xorg session type in XRDP login screen |
| Session drops | Timeout settings | On the server: `echo 'MaxStartups 100:30:200' | sudo tee /etc/xrdp/xrdp.ini` |
