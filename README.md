# From Blocking Ads to Building Infrastructure

### The evolution of my homelab, network, and technical skills

My homelab didn't begin as an attempt to build an enterprise environment.

It started with a simple problem: I wanted better control over advertising and DNS on my home network without relying entirely on cloud-based filtering services.

What started as a repurposed laptop running Pi-hole gradually evolved into an environment where I could experiment with networking, Linux, self-hosting, virtualization, monitoring, security, and automation.

Each generation of the lab has been driven by either a problem I wanted to solve, something new I wanted to learn, or a limitation I encountered in the previous design.

This repository documents that evolution.

---

## Homelab Evolution

### Era 1 — Taking Control of DNS
**Pi-hole | Linux | DNS | Repurposed Hardware**

I started with a simple unmanaged Ethernet switch and repurposed a Windows laptop to run Pi-hole.

I had previously experimented with public DNS filtering, but wanted more visibility and control over what was happening on my own network. Pi-hole gave me a network-wide solution that I could operate myself.

This became my first experience maintaining a persistent Linux-based network service.

**Experience gained:** Linux fundamentals, DNS, network services, self-hosting, hardware repurposing

---

### Era 2 — Learning Managed Networking
**Cisco Switching | IOS | SSH | Device Hardening**

After beginning my career in networking, I replaced the unmanaged switch with a managed Cisco switch so I could gain additional hands-on experience at home.

The home network remained mostly flat at this stage. My focus was learning the equipment itself: configuring and monitoring interfaces, enabling SSH management, working with Cisco IOS, and practicing device-hardening techniques.

This gave me an environment where I could reinforce networking concepts outside of production systems.

**Experience gained:** Cisco IOS, managed switching, SSH, device administration, network troubleshooting, device hardening

---

### Era 3 — Building My Own Network Edge
**pfSense | Routing | Firewalling | NAT**

After discovering that pfSense could run on repurposed hardware, I realized I could experiment with a more capable firewall without purchasing a dedicated appliance.

I converted another existing laptop into a pfSense firewall/router and began experimenting with routing, firewall policies, NAT, DHCP, and greater control over the network edge.

This was an important transition for the lab: instead of only hosting services on my network, I was now experimenting with the infrastructure that made the network operate.

**Experience gained:** Routing, firewall policy, NAT, DHCP, network security, infrastructure troubleshooting

---

### Era 4 — Discovering Self-Hosting
**Ubuntu Server | AdGuard Home | Docker**

Experimenting with pfSense made me start looking for other services and infrastructure that I could operate myself.

Having previously used AdGuard on mobile devices, I discovered AdGuard Home and decided to replace Pi-hole with it. I repurposed another Windows laptop as an Ubuntu Server, providing a permanent Linux platform for AdGuard Home and future services.

Once the Ubuntu server existed, the question quickly changed from:

> "What can replace Pi-hole?"

to:

> **"What else can I self-host?"**

The server gradually became a platform for Docker containers, Home Assistant, monitoring tools, and other experiments.

**Experience gained:** Linux server administration, SSH, Docker, Docker Compose, DNS administration, application hosting, service management

---

### Era 5 — Bringing Enterprise Networking Home
**FortiGate | Cisco | VLANs | Segmentation**

As my networking experience grew, I began applying more enterprise networking concepts to the homelab.

The environment evolved toward FortiGate firewalling and Cisco managed switching, allowing me to work with VLANs, trunking, firewall policies, NAT, intentional IP addressing, and network segmentation.

The homelab increasingly became a place where I could reinforce professional networking skills while experimenting with designs and technologies outside of a production environment.

**Experience gained:** FortiGate, Cisco networking, VLANs, trunking, segmentation, firewall policy, NAT, IP architecture

---

### Era 6 — Hosting a Real Workload
**Dedicated Game Server | Docker | NAT | Resource Planning**

While playing a multiplayer game with a friend, we wanted a persistent private server. Initially, I subscribed to a hosted game-server provider.

After reviewing the resources available on my Ubuntu server, I realized it had enough unused capacity to host the server locally instead.

I deployed the dedicated server as a container and began managing its networking, persistent data, updates, and availability myself.

This was an interesting change for the homelab. It was no longer used only for experimentation — another person was now depending on a service running on my infrastructure.

**Experience gained:** Containerized application hosting, resource planning, port forwarding/NAT, persistent storage, service availability, application troubleshooting

---

### Era 7 — Moving to Virtualized Infrastructure
**HPE ProLiant | Proxmox VE | ZFS | VMs | LXC**

I eventually acquired a used HPE ProLiant server that someone was getting rid of.

I initially explored recovering the existing Windows-based environment, but after investigating the existing installation and licensing requirements, I determined that restoring it wasn't a practical long-term solution.

Instead, I researched virtualization platforms, wiped the existing environment, and installed Proxmox VE.

Rather than simply moving the Ubuntu installation to more powerful hardware, this provided an opportunity to redesign the environment.

Services that had accumulated on one Linux server could now be separated into purpose-specific virtual machines and containers with dedicated resources and clearer roles.

**Experience gained:** Proxmox VE, virtualization, KVM, LXC, ZFS, storage administration, migration planning, workload isolation, resource allocation

---

### Era 8 — Operating Infrastructure
**Monitoring | Backups | Remote Access | Automation**

Once the environment was virtualized, my focus began shifting from simply deploying services to operating them reliably.

I introduced centralized monitoring, external health checks, scheduled backups, secure remote access, SSH-based administration, dedicated service accounts, and automated management workflows.

The question changed again.

Instead of:

> "How do I get this running?"

I started asking:

> **"How do I know it's healthy, secure it, maintain it, automate it, and recover it when something fails?"**

**Experience gained:** Infrastructure monitoring, observability, backup and recovery, secure remote access, SSH, Bash automation, service accounts, operational troubleshooting

---

### Era 9 — Current: Segmentation, Local Control & Automation
**Home Assistant | IoT | Matter | Z-Wave | Security**

The current phase of the lab is focused on improving segmentation between trusted clients, servers, management infrastructure, and IoT devices while maintaining the communication required between them.

I'm also working toward reducing unnecessary cloud dependencies in my smart-home environment by moving more functionality toward Home Assistant and locally controlled technologies.

At the same time, I'm continuing to improve monitoring, automation, backup strategies, remote administration, and infrastructure documentation.

**Currently exploring:** IoT segmentation, Matter, Z-Wave, Home Assistant, cross-VLAN services, least-privilege access, infrastructure automation, monitoring and alerting

---

## Current Environment

The current homelab combines networking, virtualization, self-hosted services, monitoring, automation, and smart-home infrastructure.

### Networking

- FortiGate firewall
- Cisco managed switching
- VLAN segmentation
- Firewall policy and NAT
- Dedicated infrastructure addressing
- Tailscale remote access

### Virtualization & Systems

- Proxmox VE
- HPE ProLiant server
- ZFS storage
- Linux virtual machines
- Linux containers (LXC)
- Docker / Docker Compose

### Infrastructure Services

- AdGuard Home
- Home Assistant
- Beszel monitoring
- External health monitoring
- Dedicated game server
- Tailscale subnet routing

### Operations & Automation

- Scheduled VM/LXC backups
- Infrastructure monitoring and alerting
- SSH key-based administration
- Dedicated service accounts
- Bash management scripts
- Remote service management
- Home Assistant infrastructure controls

---

## Current Architecture

> Architecture diagram coming soon.

One of the next goals for this repository is to document the current network and virtualization architecture while keeping sensitive information out of the public documentation.

---

## Projects & Case Studies

As this portfolio grows, individual projects will be documented in greater detail.

Planned documentation includes:

- Ubuntu Server → Proxmox migration
- AdGuard Home deployment
- Tailscale remote-access architecture
- Network segmentation and VLAN design
- Homelab monitoring and alerting
- Backup and recovery strategy
- Dedicated game-server hosting
- Home Assistant infrastructure integration
- IoT and smart-home segmentation

---

## What I'm Working On

The homelab is intentionally a work in progress.

Current areas of development include:

- Improving IoT network segmentation
- Expanding local smart-home control
- Improving monitoring and alerting
- Refining backup and recovery procedures
- Automating routine infrastructure management
- Improving infrastructure documentation
- Continuing to explore enterprise networking and systems technologies

---

## About This Repository

This repository is intended to document both **what I built and why I built it**.

Configurations, diagrams, scripts, and examples published here are sanitized before being made public. Credentials, private keys, tokens, public-facing identifiers, and other sensitive infrastructure information are intentionally excluded.

The goal isn't to present the homelab as a finished product.

It's to document the process of continually learning, identifying limitations, designing solutions, and improving the environment over time.
