# Era 5 of 9 — Hosting a Real Workload

**Game server · Docker · NAT · Resource planning**

## A service someone depended on
A friend and I wanted a persistent private game server. I first subscribed to a hosted provider, then checked the spare CPU and memory on my Ubuntu server and found enough capacity to host it myself.

I deployed the game server in a container and managed its networking, persistent data, updates, and resource use.

## What changed
The lab now supported a service another person actively used. That made uptime, maintenance, troubleshooting, and backups more concrete.

## What I learned
**Containerized hosting · Docker · Port forwarding · NAT · Persistent storage · Resource planning**

## Why the lab grew
More services and more experience with networking led me to apply enterprise networking ideas at home, including segmentation and clearer trust boundaries.

**Previous:** [Era 4 — Discovering Self-Hosting](04-self-hosting.md)  
**Next:** [Era 6 — Bringing Enterprise Networking Home →](06-enterprise-networking.md)

[← Evolution index](README.md)
