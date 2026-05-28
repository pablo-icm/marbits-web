---
title: Getting Started
summary: Everything you need to know to set up your account and connect to MARBITS for the first time.
date: 2024-01-01
weight: 10
show_breadcrumb: true
---

{{< toc >}}

Welcome to MARBITS! This page walks you through everything you need to start computing.

---

## Requisites

Before you can use MARBITS you will need:

1. **A MARBITS user account** — associated to at least one project/bank account for billing purposes. You or your supervisor must send an email to jlruiz (@icm.blablabla) requesting the account and specifying the project(s) it will be billed to.

2. **Access to the CMIMA local network** — MARBITS is only reachable from within the [CMIMA](http://www.cmima.csic.es/) network. You need to have your computer authorised by IT to access it (antivirus protection, etc). If you have any trouble open a [ticket at the ICM intranet](https://sau.cmima.csic.es/otrs/customer.pl).

3. **Remote access via VPN or `salamandra`** — If you work remotely, you can access all local netowrk resources through the VPN. If you are not a CSIC employee, you need an account on the `salamandra` gateway server. [Ask IT for either one](https://sau.cmima.csic.es/otrs/customer.pl). See [Accessing from outside CMIMA](#accessing-from-outside-cmima) below.

4. **A terminal app** — Linux and macOS users are all set. Windows users can install [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) or use Windows Subsystem for Linux (WSL).

---

## Logging in

From a terminal on the CMIMA network:

```bash
ssh your_username@marbits.cmima.csic.es
```

The first time you log in, change your default password immediately:

```bash
passwd
```

---

## First steps & rules

MARBITS is a shared HPC cluster. A few rules keep it running smoothly for everyone:

{{% callout warning %}}
**Never run jobs on the head/login node (`marbits`).** Jobs there will be killed without warning. Always use SLURM to submit work to the compute nodes. See [Running Jobs](/docs/running-jobs/).
{{% /callout %}}

- **Your `/home` is small** — it has a soft quota of **7 GB** (hard: 6 GB). Store only configuration files and small scripts there. All data should go to the [Lustre filesystem](/docs/filesystem/).

- **Use `/mnt/smart/scratch/your-group-folder` for job output** — this area has no backups and files older than 3 months are bound to be automatically deleted. Move anything you want to keep to any other storage or backup solution you may have.

- **Use scratch, not home, for job writes** — writing large amounts of data to `/home` degrades cluster performance. Again: **Use scratch!**.

- **Delete what you no longer need** — storage is finite. Also, download or copy input files from an external source to scratch and delete them as soon as the calculations are done.

- **Repeat: don't run jobs on the head node** — it is heavily monitored and processes will be killed.

---

## Accessing from outside CMIMA
If you have a VPN active, you are good to go.

To connect to MARBITS from outside the CMIMA network using `salamandra`:

1. Log in to the `salamandra` gateway server (ask IT for an account if you don't have one):
   ```bash
   ssh your_username@salamandra.cmima.csic.es
   ```

2. From `salamandra`, SSH into MARBITS normally:
   ```bash
   ssh your_username@marbits.cmima.csic.es
   ```

Alternatively, you can set up an SSH tunnel for file transfers. See [File Transfer](/docs/file-transfer/) for details.

---

## Learning the command line

MARBITS has no graphical interface — everything is done via the command line. If you are new to the Unix shell, here are some resources:

- [Software Carpentry – Unix Shell](https://swcarpentry.github.io/shell-novice/) — excellent free tutorial
- [MARBITS shell introduction (PDF)](https://gitlab.com/MARBIOS/resources/blob/master/Presentations/Shell_handout.pdf) — short and to the point

The MARBITS community occasionally organises **LaPera Sessions** — short bioinformatics seminars for beginners. Ask on the [Discussions](https://github.com/marbits-icm/marbits-public/discussions) channel.

---

## Next steps

| Step | Link |
|---|---|
| Understand the hardware | [System Overview](/docs/system-overview/) |
| Learn about storage | [File System](/docs/filesystem/) |
| Submit your first job | [Running Jobs](/docs/running-jobs/) |
| Load software modules | [Software Environment](/docs/software/) |
| Transfer files | [File Transfer](/docs/file-transfer/) |
| Common questions | [FAQ](/docs/faq/) |
