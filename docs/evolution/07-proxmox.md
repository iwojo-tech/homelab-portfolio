# Era 7 of 9 — Moving to Virtualized Infrastructure

**HPE ProLiant · Proxmox VE · ZFS · KVM/QEMU · LXC**

## A new platform
I acquired a used HPE ProLiant server with an existing Windows-based environment. After reviewing the installation and licensing requirements, I decided a recovery was not a practical long-term plan.

I researched virtualization platforms, wiped the old installation, and installed Proxmox VE.

<p align="center">
  <img src="../../images/ProxmoxDashboard.png" alt="Proxmox dashboard" width="720">
</p>

## What changed
Instead of moving one crowded Ubuntu server onto more powerful hardware, I separated services into purpose-built virtual machines and containers with clearer roles and dedicated resources.

The environment now uses KVM/QEMU virtual machines and LXC containers for workloads such as AdGuard Home, Beszel, Tailscale routing, Home Assistant, and game-server hosting.

## What I learned
**Proxmox VE · Virtualization · ZFS · Storage · Resource allocation · Workload isolation · Migration and backup planning**

## Why the lab grew
Virtualization made deployment easier to organize. Operating several systems made it more important to know when they were healthy and how to recover them.

**Previous:** [Era 6 — Bringing Enterprise Networking Home](06-enterprise-networking.md)  
**Next:** [Era 8 — Operating Infrastructure →](08-operations.md)

[← Evolution index](README.md)
