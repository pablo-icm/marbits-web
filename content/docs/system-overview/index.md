---
title: System Overview
summary: Hardware description, compute nodes, network and storage at a glance.
date: 2024-01-01
weight: 20
show_breadcrumb: true
---

{{< toc >}}

MARBITS is built around a High Performance Computing (HPC) cluster physically located in the CPD room of the **Centre Mediterrani d'Investigacions Marines i Ambientals (CMIMA)**, next to the Somorrostro beach in Barcelona.

---

## At a glance

| Resource | Value |
|---|---|
| Compute nodes | 22 |
| CPU cores (physical) | 396 |
| CPU cores (with hyperthreading) | 792 |
| Total RAM | ~4.6 TB |
| Storage (Lustre) | ~800 TB classic + 220 TB Smart |
| Job scheduler | SLURM |
| OS | CentOS 7.5 (OpenHPC) |

---

## Login / Master node

The master and login node is called **`marbits`**. It is a **Fujitsu Primergy RX2530 M2** server with:

- 2 × Intel Xeon E5-2603v4 processors
- 2 × 240 GB SSD disks
- 64 GB RAM
- CentOS 7.5 with OpenHPC and SLURM

{{% callout warning %}}
The master node is **not** a compute node. Do not run analyses there.
All computation must go through [SLURM](/docs/running-jobs/).
{{% /callout %}}

The master node is reachable only from within the CMIMA local network.

---

## Compute nodes

The 22 compute nodes are divided into three classes:

### Class A — Supermicro standard (8 nodes)

Deployed in 2 Twin systems (2× SYS-2028TP-HTR of 4 nodes each):

| Feature | Value |
|---|---|
| Nodes | 8 |
| CPU | 2 × Intel Xeon E5-2650v4 (12 cores each) |
| Cores per node | 24 physical |
| Total cores | 192 physical |
| RAM per node | 256 GB |
| Total RAM | 2,048 GB |
| Hyperthreading | No |

### Class B — Supermicro high-memory (2 nodes)

Deployed in 1 Twin system (SYS-2028TP-HTR+). Built for memory-hungry tasks such as **metagenome assembly**:

| Feature | Value |
|---|---|
| Nodes | 2 (+ 2 barebones expandable) |
| CPU | 2 × Intel Xeon E5-2650v4 (12 cores each) |
| Cores per node | 24 physical |
| Total cores | 48 physical |
| RAM per node | **772 GB** |
| Total RAM | 1,544 GB |
| Hyperthreading | No |

### Class C — IBM dx360 M3 (12 nodes)

| Feature | Value |
|---|---|
| Nodes | 12 |
| CPU | 2 × 6-core Intel X5650 @ 2.66 GHz |
| Cores per node | 12 physical |
| Total cores | 144 physical |
| RAM per node | 80 GB |
| Total RAM | 960 GB |
| Disk | 1 × 250 GB 7.2K RPM |

---

## Network

| Network | Speed | Switch | Purpose |
|---|---|---|---|
| Storage (Lustre) | **10 Gbps** | Netgear XS748T | High-speed data I/O |
| HPC interconnect | 1 Gbps | SMC8150L2 | Node–node communication |
| Management | 1 Gbps | SMC8150L2 | Admin/monitoring |

---

## Storage

See the [File System](/docs/filesystem/) page for full details on the Lustre filesystem, quotas, and storage best practices.
