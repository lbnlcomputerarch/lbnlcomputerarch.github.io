---
layout: page
title: VNC Remote GUI
permalink: /docs/vnc-tunnel/
---

## VNC Remote GUI

This guide covers accessing a remote graphical desktop through VNC, using an SSH tunnel for encryption. SSH tunneling ensures that the VNC traffic — which is not encrypted by default — is transmitted securely.

## Prerequisites

- SSH access to our servers (see [SSH Access]({{ site.baseurl }}/docs/ssh-access/))
- A VNC viewer on your local machine
    - **macOS**: Built-in "Screen Sharing" (Type `vnc://` in Safari's address bar) or [RealVNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)
    - **Windows**: [RealVNC Viewer](https://www.realvnc.com/en/connect/download/viewer/), [TigerVNC](https://github.com/TigerVNC/tigervnc/releases)
    - **Linux**: `xtigervncviewer`, `remmina`, or [TigerVNC](https://github.com/TigerVNC/tigervnc/releases)

## Step 1 — Configure VNC

Set up your VNC password (this is separate from your system password):

```bash
vncpasswd
```

Configure the desktop environment. Create or edit `~/.vnc/xstartup`:

```bash
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
```

Then make it executable:

```bash
chmod +x ~/.vnc/xstartup
```

## Step 2 — Start a VNC Session

Start a VNC server session on a specific display/port:

```bash
vncserver :1 -geometry 1920x1080 -depth 24
```

- `:1` assigns **port 5901** (5900 + display number)
- `-geometry` sets the desktop resolution — adjust to your preference
- `-depth` sets color depth (24-bit is fine for most uses)

To list active sessions:

```bash
vncserver -list
```

To kill a session:

```bash
vncserver -kill :1
```

## Step 3 — Create an SSH Tunnel

On your local machine, open an SSH tunnel from a local port to your VNC display:

```bash
ssh -L 59020:localhost:5901 USERNAME@SERVER.HOSTNAME.lbl.gov
```

| Port in command | Meaning |
|-----------------|---------|
| `59020` | The port on **your machine** that forwards traffic |
| `5901` | The port on the **remote server** where VNC is listening |

- Keep this terminal window open for the duration of your session
- Close it when you are done to close the tunnel

You can add this to `~/.ssh/config`:

```
Host cag-vnc
    HostName SERVER.HOSTNAME.lbl.gov
    User USERNAME
    LocalForward 59020 localhost:5901
    IdentityFile ~/.ssh/id_ed25519
```

Then run:

```bash
ssh cag-vnc
```

## Step 4 — Connect with Your VNC Viewer

Open your VNC client and connect to:

```
localhost:59020
```

You will be prompted for:

1. Your VNC password (set in Step 2)
2. Optionally, your system username and password

Once connected, you will see the remote desktop.

## Running Multiple VNC Sessions

You can run multiple VNC sessions on different display numbers and ports:

```bash
# Session 1 — port 5902 (display :2)
vncserver :2 -geometry 1920x1080

# Session 2 — port 5903 (display :3)
vncserver :3 -geometry 2560x1440
```

Then create separate SSH tunnels for each:

```bash
# Tunnel for session 1
ssh -L 59021:localhost:5902 USERNAME@SERVER.HOSTNAME.lbl.gov

# Tunnel for session 2
ssh -L 59022:localhost:5903 USERNAME@SERVER.HOSTNAME.lbl.gov
```

## Troubleshooting

| Problem | Possible cause | Solution |
|---------|---------------|----------|
| VNC server fails to start | Another session running or lock file | Run `vncserver -kill :1` then `rm ~/.vnc/*.log ~/.vnc/xorg-*` |
| Black or blank screen | `xstartup` misconfigured | Verify `~/.vnc/xstartup` contains `startxfce4 &` and is executable |
| Connection refused by tunnel | Tunnel not open or wrong port | Confirm the SSH tunnel is running; check the display number maps to the right port (5900 + display) |
| VNC viewer prompts for wrong password | Desktop vs VNC password | Use the password you set with `vncpasswd`, not your system password |
| Screen is too small | Default geometry | Start VNC with `-geometry` set to your screen resolution |

## Auto-Starting VNC on Login

To have VNC start automatically when your session begins, add it to `~/.bashrc`:

```bash
# Start VNC if not already running
if [ -z "$(vncserver -list 2>/dev/null | grep ':1')" ]; then
    vncserver :1 -geometry 1920x1080 -depth 24
fi
```

## Cleanup

```bash
# Stop a VNC session
vncserver -kill :1

# Stop all sessions
vncserver -kill :1
vncserver -kill :2
# or kill all:
for display in $(vncserver -list | grep -o ':[0-9]*'); do
    vncserver -kill $display
done
```
