---
title: File System
summary: Description of MARBITS file systems, storage quotas, and best practices.
date: 2024-01-01
weight: 30
show_breadcrumb: true
---

{{< toc >}}

MARBITS provides several filesystems with different performance and durability characteristics. Choosing the right one for your work is important for both performance and data safety.

---

## Quick reference

| Filesystem | Path | Use for | Backed up? | Notes |
|---|---|---|---|---|
| Home | `/home/<user>` | Config files, scripts | Yes | Tiny quota — keep it light |
| Lustre "Classic" | `/mnt/lustre` | Computation & user data | Yes | ⚠ Currently unreliable |
| Lustre "Smart" | `/mnt/smart` | **Active computation** | Limited | Preferred currently |
| Lustre Scratch | `/mnt/lustre/scratch` | Temporary job output | **No** | Auto-deleted after 3 months |
| Lustre Repos | `/mnt/lustre/repos` | Public/redownloadable datasets | No | Read-only |
| Biostore | `/mnt/biostore` | Data archival | No | NFS — not for computation |
| Cold02 | `/mnt/cold02` | Long-term storage | No | NFS — not for computation |

---

## `/home` filesystem

Your home directory (`/home/<username>`) is a soft link pointing to your personal directory inside the Lustre filesystem. The underlying `/home` volume is **shared by all users and is very small (~150 GB total).**

Keep it lean — only configuration files (`.bashrc`, `.ssh/`, etc.) and small scripts.

### Quota on `/home`

| Quota type | Limit |
|---|---|
| Soft quota | **2.5 GB** (7-day grace period) |
| Hard quota | **3 GB** (cannot be exceeded) |

Check your current usage:

```bash
quota
```

---

## Lustre filesystem

MARBITS mounts two [Lustre](http://lustre.org/) parallel filesystems (`/mnt/lustre` and `/mnt/smart`) shared with other HPC services at CMIMA. Lustre provides parallel, high-speed access distributed across multiple storage servers.

{{% callout warning %}}
**`/mnt/lustre` is currently unreliable.** Please use `/mnt/smart` for active computation, but clean up your files as soon as possible to leave space for other users.
{{% /callout %}}

### Storage sizes

| Volume | Capacity |
|---|---|
| Classic Lustre (`/mnt/lustre`) | ~800 TB |
| Smart Lustre (`/mnt/smart`) | ~220 TB |

### Best practices

- **Write job output to `/mnt/lustre/scratch`** — when the job finishes, move what you want to keep to your personal Lustre directory. Moving within the same filesystem is instantaneous (`mv` is free).
- **Delete temporary and intermediate files** regularly. Storage is expensive and shared.
- **Compress everything you can** — many tools accept `.gz` files directly.
- **Do not run jobs from `/mnt/biostore` or `/mnt/cold02`** — these NFS mounts are not optimised for computation.

### Scratch (`/mnt/lustre/scratch`)

This is a high-speed temporary workspace. It has **no backups** and files older than **3 months** are automatically deleted by the system. Use it only for active job I/O.

### User directories

Each user has a personal directory at `/mnt/lustre/bio/users/<username>`. Your `/home` is a symlink pointing there.

Create additional symlinks to your data for convenient navigation:

```bash
ln -s /mnt/lustre/bio/users/psanchez/myproject/ ~/myproject
```

### Repos (`/mnt/lustre/repos`)

Public or re-downloadable datasets go here. It is **read-only** for regular users. Ask the admins to add datasets.

---

## NFS storage (archival)

| Path | Purpose |
|---|---|
| `/mnt/biostore` | Long-term archival — NFS, slow, not for computation |
| `/mnt/cold02` | Cold storage — NFS, for data you rarely access |

These are managed separately from Lustre. Do not run jobs from these volumes.

---

## More

- [Transferring files to/from MARBITS](/docs/file-transfer/)
- [Backup policy](/docs/backup/)
- [FAQ — how to make symlinks](/docs/faq/#how-do-i-make-a-link-to-my-stuff-in-mntlustrebiousersmy-user-name)
