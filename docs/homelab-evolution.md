# Homelab Evolution

## From Blocking Ads to Building Infrastructure

My homelab did not begin as an attempt to build an enterprise environment.

It started with a simple problem: like many people, I was tired of seeing ads everywhere—especially on my children's devices. I wanted a way to block ads across my entire home network without relying entirely on cloud-based services.

What started as a repurposed laptop running Pi-hole for network-wide ad blocking through DNS filtering gradually evolved into an environment for experimenting with managed networking, Linux, self-hosting, firewalls, Docker, virtualization, monitoring, remote access, security, and automation.

Each stage of the lab has been driven by one of three things:

- A problem I wanted to solve
- Something new I wanted to learn
- A limitation I discovered in the previous design

This page documents that evolution.

---

## Era 1 — Taking Control of DNS

### Pi-hole | Linux | DNS | Repurposed Hardware

The first version of the lab was simple.

I added an unmanaged Ethernet switch to my home network so I could connect a repurposed laptop running Pi-hole.

The laptop had originally been a Windows 10 system, but I converted it to Linux so I could use it as a dedicated DNS filtering server.

I had previously experimented with public DNS filtering services, but I wanted more control and visibility over what was happening on my own network.

Pi-hole gave me a network-wide solution that I could operate myself and became my first experience maintaining a persistent Linux-based network service.

### Experience gained

- Linux fundamentals
- DNS
- Network services
- Self-hosting
- Hardware repurposing
- Basic service administration

---

## Era 2 — Learning Managed Networking

### Cisco Switching | IOS | SSH | Device Hardening

After beginning my career in networking, I wanted equipment at home that would let me practice more of the concepts I was working with professionally.

I replaced the unmanaged switch with a managed Cisco switch.

At this stage, I did not immediately redesign the network or introduce extensive VLAN segmentation. My focus was learning the switch itself.

I configured remote management, enabled SSH access, monitored interfaces, worked with Cisco IOS, and practiced basic device-hardening techniques.

This gave me a place to reinforce networking concepts outside of production systems without the risk of affecting business operations.

### Experience gained

- Cisco IOS
- Managed switching
- SSH
- Interface management
- Device administration
- Basic hardening
- Network troubleshooting

---

## Era 3 — Building My Own Network Edge

### pfSense | Routing | Firewalling | NAT

After learning that pfSense could run on repurposed hardware, I realized I could experiment with a more capable firewall without purchasing a dedicated appliance.

I repurposed another older Windows laptop and converted it into a pfSense firewall and router.

This expanded the homelab beyond switching and DNS filtering and gave me more direct control over the network edge.

I began working with routing, firewall rules, NAT, DHCP, and general network security concepts in a hands-on environment.

This was an important transition because I was no longer only hosting services on the network—I was now experimenting with the infrastructure responsible for moving and controlling traffic.

### Experience gained

- Routing
- Firewall policy
- NAT
- DHCP
- Network security
- Network edge administration
- Infrastructure troubleshooting

---

## Era 4 — Discovering Self-Hosting

### Ubuntu Server | AdGuard Home | Docker

Experimenting with pfSense made me start looking for other services and infrastructure I could operate myself.

Having previously used AdGuard on mobile devices, I discovered AdGuard Home and decided to replace Pi-hole with it.

I repurposed another Windows laptop as an Ubuntu Server, giving me a more flexible Linux platform for AdGuard Home and future services.

Once the Ubuntu server existed, the question quickly changed from:

> "What can replace Pi-hole?"

to:

> **"What else can I self-host?"**

That server gradually became the platform for additional services, Docker containers, Home Assistant, monitoring tools, and other experiments.

This stage was where the homelab began expanding from a few network utilities into a more general-purpose server environment.

### Experience gained

- Ubuntu Server
- Linux administration
- SSH
- AdGuard Home
- DNS administration
- Docker
- Docker Compose
- Application hosting
- Service management
- Self-hosted infrastructure

---

## Era 5 — Hosting a Real Workload

### Dedicated Game Server | Docker | NAT | Resource Planning

While playing a multiplayer game with a friend, we wanted a persistent private game server.

Initially, I subscribed to a hosted game-server provider.

After reviewing the available CPU and memory on my Ubuntu server, I realized I had enough unused capacity to host the server myself.

I deployed the game server as a container and began managing its networking, persistent data, updates, resource usage, and availability.

This was an interesting shift for the lab.

Up to that point, most of the environment existed primarily for learning and personal use. Now another person was actively depending on a service running on my infrastructure.

That introduced a different mindset around uptime, maintenance, troubleshooting, backups, and change management.

### Experience gained

- Containerized application hosting
- Docker
- Resource planning
- Port forwarding
- NAT
- Persistent storage
- Application troubleshooting
- Service availability
- Maintenance planning

---

## Era 6 — Bringing Enterprise Networking Home

### FortiGate | Cisco | VLANs | Segmentation

As my professional networking experience grew, I began applying more enterprise networking concepts to the homelab.

The environment evolved to include a FortiGate firewall and managed Cisco switching.

This gave me the ability to work with VLANs, trunking, firewall policies, NAT, network segmentation, and more intentional IP addressing.

Rather than treating the home network as one large flat network, I began thinking about infrastructure in terms of roles, trust boundaries, management access, servers, clients, and IoT devices.

The homelab became a place where I could reinforce professional networking skills while experimenting with designs and technologies outside of a production environment.

### Experience gained

- FortiGate administration
- Cisco networking
- VLANs
- Trunking
- Access ports
- Network segmentation
- Firewall policy
- NAT
- IP addressing
- Network design

---

## Era 7 — Moving to Virtualized Infrastructure

### HPE ProLiant | Proxmox VE | ZFS | KVM/QEMU | LXC

I eventually acquired a used HPE ProLiant server that someone was getting rid of.

The server already had an existing Windows-based environment installed, so I initially investigated whether I could recover and reuse it.

After looking into the existing configuration and licensing requirements, I decided that restoring the environment was not a practical long-term solution.

Instead, I researched virtualization platforms, wiped the existing installation, and installed Proxmox VE.

Rather than simply moving the Ubuntu server to more powerful hardware, I used the opportunity to redesign the environment.

Services that had accumulated on a single Linux server could now be separated into purpose-built virtual machines and containers with dedicated resources and clearer roles.

The current environment uses both KVM/QEMU virtual machines and LXC containers through Proxmox VE.

Examples include dedicated systems for:

- AdGuard Home
- Beszel monitoring
- Tailscale routing
- Home Assistant
- Dedicated game-server hosting

This stage also introduced more structured storage, backup, and recovery planning.

### Experience gained

- Proxmox VE
- Virtualization
- KVM/QEMU virtual machines
- LXC containers
- ZFS
- Storage administration
- Resource allocation
- Workload isolation
- Migration planning
- Backup planning

---

## Era 8 — Operating Infrastructure

### Monitoring | Backups | Remote Access | Automation

Once the environment was virtualized, my focus began shifting from simply deploying services to operating them reliably.

The question changed from:

> "How do I get this running?"

to:

> **"How do I know it is healthy, maintain it, secure it, automate it, and recover it when something fails?"**

I began adding centralized monitoring, external health checks, scheduled backups, secure remote access, SSH-based administration, dedicated service accounts, and management automation.

Beszel provides centralized visibility into system resource usage and service health across multiple hosts.

Healthchecks.io gives me an external method of confirming that critical systems are still able to reach the internet and report their status.

Tailscale provides secure remote access to internal services without exposing management interfaces directly to the public internet.

I also began building Bash scripts and Home Assistant controls to simplify common infrastructure tasks such as checking server status, restarting services, and performing controlled updates.

### Experience gained

- Infrastructure monitoring
- Observability
- Backup and recovery
- Secure remote access
- Tailscale
- SSH key-based administration
- Dedicated service accounts
- Bash scripting
- Service management
- Operational troubleshooting
- Infrastructure automation

---

## Era 9 — Local Control, Segmentation, and Automation

### Home Assistant | IoT | Matter | Z-Wave | Security

The current phase of the homelab is focused on improving how the environment is segmented, managed, and automated.

One major area of development is separating trusted clients, servers, management infrastructure, and IoT devices while maintaining the communication required between them.

I am also working toward reducing unnecessary cloud dependencies in my smart-home environment by moving more functionality toward Home Assistant and locally controlled technologies.

Home Assistant has also become useful beyond smart-home automation.

I have built a custom management dashboard that allows me to view server status, check uptime, initiate controlled restart and update actions, and quickly access tools such as Proxmox, AdGuard Home, Beszel, and external health monitoring.

This brings together several areas of the lab—Linux, SSH, scripting, Docker, monitoring, networking, and automation—into a single operational workflow.

### Currently exploring

- IoT network segmentation
- Matter
- Z-Wave
- Home Assistant
- Cross-VLAN services
- Least-privilege access
- Local-first smart-home design
- Infrastructure automation
- Monitoring and alerting
- Backup and recovery improvements

---

## Current Environment

Today, the homelab combines networking, virtualization, self-hosted services, monitoring, automation, and smart-home infrastructure.

The current environment includes technologies such as:

- FortiGate
- Cisco managed switching
- VLAN segmentation
- Proxmox VE
- KVM/QEMU
- LXC
- ZFS
- Linux
- Docker
- Docker Compose
- AdGuard Home
- Home Assistant
- Beszel
- Tailscale
- Healthchecks.io
- SSH
- Bash scripting

The environment continues to evolve as I identify new problems to solve, technologies to learn, and opportunities to improve how the infrastructure is designed and operated.

---

## What This Project Represents

The goal of this homelab has never been to recreate a production enterprise environment at home.

It is a practical learning environment where I can experiment, make mistakes, troubleshoot problems, test ideas, and better understand the technologies I work with.

The most valuable part of the project has been the progression itself.

Each new tool or design decision has introduced another layer of networking, systems administration, security, automation, or operational thinking.

What began as a way to block ads across my home network has become an ongoing platform for learning how infrastructure is designed, operated, monitored, secured, and improved.
