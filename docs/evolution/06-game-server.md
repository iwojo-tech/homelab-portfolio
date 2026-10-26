# Era 6 — Hosting a Real Workload

**RuneScape: Dragonwilds · Docker · NAT · Persistent storage**

## A service someone depended on
A friend and I wanted a persistent private game server. I started with a paid hosting provider, then looked at the unused CPU and memory on my Ubuntu server and decided to host it myself.

I deployed the Dragonwilds dedicated server in a container and managed its connectivity, persistent data, resource use, and updates.

## What changed
- The home lab now ran a service another person actively used.
- Port forwarding and NAT had a practical purpose: allowing a friend to connect remotely.
- Updates, backups, and troubleshooting had to account for players' progress and server availability.
- I began paying closer attention to CPU, memory, and the difference between a process starting and a game server actually being ready.

## Skills Applied & Developed
- **Applied:** Networking, NAT, connectivity troubleshooting, and capacity awareness.
- **Expanded:** Docker-based game hosting, persistent application data, update procedures, resource monitoring, and maintaining a service for remote users.

<p align="center">
  <a href="../../images/ChatGPT%20Image%20Oct%207%2C%202026%2C%2010_38_00%20AM.png">
    <img src="../../images/ChatGPT%20Image%20Oct%207%2C%202026%2C%2010_38_00%20AM.png" alt="Beszel container view showing Dragonwilds CPU, memory, and uptime" width="720">
  </a>
</p>

<p align="center"><em>A later Beszel view of the Dragonwilds container, showing the resource use and uptime I track while operating the game server.</em></p>

## Why the lab grew
As I hosted more services, I needed clearer workload boundaries, storage planning, and recovery options. Virtualization was the next step.

**Previous:** [Era 5 — Bringing Enterprise Networking Home](05-enterprise-networking.md)  
**Next:** [Era 7 — Moving to Virtualized Infrastructure →](07-proxmox.md)

[← Evolution index](README.md)
