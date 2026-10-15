# Era 9 — Local Control, Segmentation, and Automation

**Home Assistant · IoT · Local-first design · Future improvements**

## The current phase
This era is an evolving record of where I want to take the homelab next, not a claim that every planned improvement has already been implemented.

My priorities include reducing unnecessary cloud dependencies, improving separation between trusted clients and IoT devices, and making everyday management easier.

<p align="center">
  <a href="../../images/homeassistant_dashboard_v2.png">
    <img src="../../images/homeassistant_dashboard_v2.png" alt="Home Assistant dashboard with Dragonwilds controls, service shortcuts, and UPS monitoring" width="720">
  </a>
</p>

<p align="center"><em>The current Home Assistant dashboard combines server controls, service shortcuts, and UPS status.</em></p>

## What is already in place
Home Assistant now provides a custom dashboard with server status and uptime, controlled maintenance actions for Dragonwilds, and links to services such as Proxmox, AdGuard Home, Beszel, and external health monitoring.

## What I am exploring
- Separating trusted clients, servers, management devices, and IoT equipment while preserving needed communication.
- Bringing more smart-home devices under local Home Assistant control.
- Evaluating Matter, Zigbee, and Z-Wave integrations and the hardware they require.
- Improving least-privilege access, monitoring, recovery, and maintenance workflows.

## Skills Applied & Developed
- **Applied:** Network segmentation design, firewall troubleshooting, service administration, and security principles.
- **Expanding and exploring:** Home Assistant integrations, local-first smart-home architecture, cross-VLAN device communication, and practical automation.

## Project writeups

As I make improvements during this era, I document each project on its own page: what I wanted to achieve, how the approach changed, how I validated the result, and what I learned. This section grows as the work develops, while the goals above remain a roadmap.

- [Dragonwilds maintenance automation](../dragonwilds-maintenance-automation.md) — how a simple SSH restart button grew into a remote maintenance workflow with backups, progress reporting, and application readiness checks.
- [AdGuard Home 1.0 beta upgrade](../adguardHome-1.0%20beta%20upgrade.md) — recovering from failed reinstall attempts and completing an upgrade while preserving configuration and history.

- [CyberPower UPS monitoring recovery](../cyberpower-ups-monitoring-recovery.md) — restoring PowerPanel telemetry after USB HID failures and finding the competing NUT driver that kept restarting.

## The journey so far
A repurposed laptop running Pi-hole grew into a platform for networking, Linux, self-hosting, virtualization, monitoring, and automation. Some projects taught me new technologies; others gave me a place to apply and strengthen skills from my professional work.

**Previous:** [Era 8 — Operating Infrastructure](08-operations.md)

[← Evolution index](README.md)
