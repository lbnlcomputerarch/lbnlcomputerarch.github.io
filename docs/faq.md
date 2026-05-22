---
layout: page
title: FAQ
nav_order: 5
permalink: /docs/faq/
parent: Documentation
---

## Frequently Asked Questions

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Access & Authentication

### How do I get an CAG account?

All accounts must be requested through the [CAG System Adminstrator](mailto:{{ 'ffard@lbl.gov' | encode_email }}).

### How do I change my CAG password?

Log into the server you have been given access and run:

```bash
passwd
```

### I forgot my CAG password. What do I do?

Contact the [CAG SysAdmin](mailto:{{ 'ffard@lbl.gov' | encode_email }}) to request a password reset.

### I can't connect via SSH from outside LBNL.

LBNL IT's Firewall can be aggressive if it sees too many connections from unknown IP addresses. Follow the instructions found on LBL's [Blocked Access to the Lab Network](https://it.lbl.gov/blocked-access-to-the-lab-network/) page.

## Computing Resources

### What servers do we have access to?

For a full list of available systems, check the [resources]({{ site.baseurl }}/resources/) page.

## Remote GUI Access

### XRDP vs VNC — which should I use?

- **XRDP** gives you a full remote desktop session and works well on most systems
- **VNC** is lighter-weight and gives you more control over individual sessions
- XRDP is generally more user-friendly; VNC gives you more flexibility

### Do I need to keep the SSH tunnel open?

Yes. The SSH tunnel encrypts the remote GUI traffic. If you close it, your GUI connection drops. If your internet drops, reconnect via SSH tunnel first, then reconnect your GUI client.

## Software & Environments

### Can I install software on our servers?

Generally, you can install tools in your home directory without `sudo` privileges. For system-wide installations, contact the [CAG SysAdmin](mailto:{{ 'ffard@lbl.gov' | encode_email }}).

## Troubleshooting

### My session keeps timing out

- Add `ServerAliveInterval 60` and `ServerAliveCountMax 3` to your `~/.ssh/config`
- Use an SSH multiplexed connection: `ssh -M -S ~/.ssh/master-%r@%h:%p SERVER`

### Disk space is full

Run `du -sh ~/* \| sort -hr | head -20` to find large directories. Clean up old environments, downloads, and temporary files.

Still stuck? [Contact our administrators](mailto:{{ 'ffard@lbl.gov' | encode_email }}) for more information.
