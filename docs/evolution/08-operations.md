# Era 8 of 9 — Operating Infrastructure

**Beszel · Healthchecks.io · Tailscale · SSH · Backups · Automation**

## From running services to operating them
With the environment virtualized, my focus shifted from **“How do I get this running?”** to **“How do I know it is healthy, maintain it, and recover it?”**

I also wanted to be able to check the lab and take quick maintenance actions when I was away from home.

## What changed
- **Beszel** provides a central view of system resources and health.
- **Healthchecks.io** provides an external signal when expected check-ins stop, including during outages that could take down local monitoring.
- **Tailscale** provides remote access without exposing management interfaces directly to the internet.
- SSH keys, dedicated accounts, and Bash scripts support controlled administration.
- Home Assistant buttons provide quick access to status, uptime, restart, and update actions for the game server.
- Scheduled Proxmox backups and recovery planning became part of routine operations.

<p align="center">
  <img src="../../images/beszeldashboard.png" alt="Beszel monitoring dashboard" width="720">
</p>

## Skills Applied & Developed
- **Applied:** Operational troubleshooting, secure remote access concepts, Linux administration, and service monitoring.
- **Expanded:** Centralized homelab monitoring, external heartbeat checks, Tailscale subnet routing, SSH-based maintenance workflows, scripting, backup scheduling, and recovery planning.

> 📷 **Image placeholder:** Sanitized Home Assistant maintenance controls or OmnySSH command-output view.

## Why the lab grew
Once I could see system health and perform maintenance more easily, I started focusing on bringing more local control and automation into the same environment.

**Previous:** [Era 7 — Moving to Virtualized Infrastructure](07-proxmox.md)  
**Next:** [Era 9 — Local Control, Segmentation, and Automation →](09-local-control.md)

[← Evolution index](README.md)
