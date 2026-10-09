# Era 5 — Hosting a Real Workload

**RuneScape: Dragonwilds · Docker · NAT · Persistent storage**

## A service someone depended on
A friend and I wanted a persistent private game server. I started with a paid hosting provider, then looked at the unused CPU and memory on my Ubuntu server and decided to host it myself.

I deployed the Dragonwilds dedicated server in a container and managed its connectivity, persistent data, resource use, and updates.

## What changed
- The homelab now ran a service another person actively used.
- Port forwarding and NAT had a practical purpose: allowing a friend to connect remotely.
- Updates, backups, and troubleshooting had to account for players' progress and server availability.
- I began paying closer attention to CPU, memory, and the difference between a process starting and a game server actually being ready.

## Skills Applied & Developed
- **Applied:** Networking, NAT, connectivity troubleshooting, and capacity awareness.
- **Expanded:** Docker-based game hosting, persistent application data, update procedures, resource monitoring, and maintaining a service for remote users.

> 📷 **Image placeholder:** Sanitized Dragonwilds server status output, container metrics, or an in-game screenshot without player identifiers.

## Why the lab grew
As I hosted more services, I wanted a more deliberate network design and clearer separation between different types of devices and workloads.

**Previous:** [Era 4 — Discovering Self-Hosting](04-self-hosting.md)  
**Next:** [Era 6 — Bringing Enterprise Networking Home →](06-enterprise-networking.md)

[← Evolution index](README.md)
