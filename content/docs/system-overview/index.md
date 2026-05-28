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
| Compute nodes | 10 |
| CPU cores (physical) | 240 |
| CPU cores (with hyperthreading) | 480 |
| Total RAM | 3.6 TB |
| Storage (Lustre) | 235 TB Smart |
| Job scheduler | SLURM |
| OS | CentOS 7.5 (OpenHPC) |

---

## Login / Master node

The master and login node is called **`marbits`**. It is a **Fujitsu Primergy RX2530 M2** server with:

- 2 × Intel Xeon E5-2603v4 processors
- 2 × 240 GB SSD disks 
- 1 x 2 TB 7200 HDD in RAID 1  
- 64 GB RAM
- CentOS 7.5 with OpenHPC and SLURM

{{% callout warning %}}
The master node is **not** a compute node. Do not run analyses there.
All computation must go through [SLURM](/docs/running-jobs/).
{{% /callout %}}

The master node is reachable only from within the CMIMA local network.

---

## Compute nodes

The 10 compute nodes are divided into two classes:

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
