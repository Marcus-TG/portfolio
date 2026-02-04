---
title: "Homelab Stack"
date: 2025-11-27
description: "A high-availability server architecture featuring Dual-WAN load balancing, 10Gb networking, and containerized orchestration."
tags: ["Docker", "TrueNAS", "Networking", "Ubuntu"]
showTableOfContents: true
---

![Server Architecture Diagram](server-diagram.svg)

## Infrastructure Overview

This project represents a two-year evolution in systems administration and networking. What started as a single virtualization node has grown into a high-availability environment featuring a **10Gb SFP+ backbone**, **Dual-WAN load balancing**, and a **containerized application core**.

### 1. Networking & Edge Security

The "brain" of the network is the **Ubiquiti Unifi Dream Machine (UDM)**.

* **Dual-WAN Load Balancing:** Configured to manage two ISP connections simultaneously, ensuring 99.9% uptime for self-hosted services and automated failover.
* **The 10Gb Core:** A **UniFi Aggregation Switch** serves as the high-speed distribution layer. It directly connects the TrueNAS storage core to the compute nodes via SFP+ DAC cables, eliminating data bottlenecks.
* **Legacy Note:** Originally managed via **OPNsense**, the move to the UDM was a strategic shift toward a unified "single pane of glass" management style while maintaining complex VLAN tagging for IoT and Server isolation.

### 2. The Storage Core (TrueNAS)

Running on a dedicated **Dell PowerEdge R710**, this node handles all data persistence for the lab.

* **File System:** ZFS (configured for bit-rot protection and snapshots).
* **Connectivity:** 10GbE direct-attach to the aggregation switch.
* **Role:** Acts as the backend for all Docker media, Immich photo libraries, and system backups.

### 3. The Application Host (Custom Whitebox)

This is a custom-built, high-performance server designed specifically for high-density container orchestration.

* **OS:** Ubuntu Server (Bare Metal).
* **Orchestration:** **Docker & Portainer**.
* **Key Services:**
  * **Traffic Management:** Nginx Proxy Manager (Handling SSL/Reverse Proxy).
  * **Automation:** **n8n** for self-hosted workflow logic.
* **Legacy Note:** This machine replaced a dedicated **Proxmox** R710 node, moving from full virtualization (VMs) to a more resource-efficient "bare-metal" container strategy.

---

### Technical Specifications Summary

| Component | Hardware | Role |
| :--- | :--- | :--- |
| **Edge Router** | Unifi UDM | Dual-WAN Load Balancing|
| **Aggregation** | Pro XG Aggregation | Aggregation Layer |
| **Switching** | Pro XG 48 PoE | Acces Layer |
| **Storage Server** | Dell R710 | Media Server/NAS |
| **App Server** | Custom Whitebox | High Performance Server |
