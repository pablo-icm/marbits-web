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
| Home | `/home/<user>` | Config files, scripts | No | Tiny quota — keep it light |
| Lustre "Classic" | `/mnt/lustre` | Computation & user data | No | ⚠ Currently unavailable |
| Lustre "Smart" | `/mnt/smart/scratch` | **Active computation** | No | Not a permanent storage volume |
| Biostore | `/mnt/biostore` | Data archival | No | NFS — not for computation |
| Cold02 | `/mnt/cold02` | Long-term storage | No | NFS — not for computation |

---

## `/home` filesystem

Your home directory (`/home/<username>`) is a soft link pointing to your personal directory inside the Lustre filesystem. The underlying `/home` volume is **shared by all users and is very small (~150 GB total).**

Keep it lean — only configuration files (`.bashrc`, `.ssh/`, etc.), maybe light conda environments and small scripts.

### Check your quota on `/home`

| Quota type | Limit |
|---|---|
| Soft quota | **6 GB** (7-day grace period) |
| Hard quota | **7 GB** (cannot be exceeded) |

Check your current usage:

```bash
quota -s
```

---

## Lustre filesystem

MARBITS used to mount two [Lustre](http://lustre.org/) parallel filesystems (`/mnt/lustre` and `/mnt/smart`) shared with other HPC services at CMIMA (namely SMART and Gaia). Lustre provides parallel, high-speed access distributed across multiple storage servers. Both lustre filesystems are managed by the Scientific Computing Service (SCS) at ICM.

{{% callout warning %}}
**`/mnt/lustre` is currently unavailable.** Please use `/mnt/smart/scratch` for active computation, but clean up your files as soon as possible to leave space for other users.
{{% /callout %}}

### Storage sizes

| Volume | Capacity |
|---|---|
| Classic Lustre (`/mnt/lustre`) | ~800 TB |
| Smart Lustre (`/mnt/smart/scratch`) | ~235 TB |

To request changes in `/mnt/smart/scratch` quotas contact jlruiz (at icm.blabla). Be aware that storage will be billed by SCS.


### Best practices

- **Copy your input files** from an external storage filesystem into `/mnt/smart/scratch/your-group` to process them. After you get your results, delete the input files (mainly if they are XL).  
- **Delete temporary and intermediate files** regularly. Storage is expensive and shared.
- **Compress everything you can** — many tools accept `.gz` files directly.
- **Do not run jobs from `/mnt/biostore` or `/mnt/cold02`** — these NFS mounts are not optimised for computation.  
- **KEEP AN OFF-PREMISES COPY OF EVERYTHING THAT YOU CANNOT ALLOW TO LOOSE!**  

{{% callout warning %}}
**Let's say it again:** At the moment, Marbits and SMART **DO NOT** offer backup services. Lustre has a redundancy layer that protects your data to some extent, but **YOU, the data owner**, are the sole and ultimate responsible of the data conservation.
{{% /callout %}}


### Group/account directories at `/mnt/smart/scratch`

Each group or `account` has a directory at `/mnt/smart/scratch/<groupName>` with a storage quota set and maintained by SCS. Your storage group should match your default computing account. 

You can create symlinks in your home directory pointing to your data for convenient navigation:

```bash
ln -s /mnt/scratch/groupName/projectName ~/projectName
```

### Check your `quota` in `/mnt/smart/scratch`

```bash
lfs quota -h -u yourUserName /mnt/smart/scratch    # to see how much space you are using
lfs quota -h -g yourGroupName /mnt/smart/scratch    # to see how much space is your group using
```


---

## NFS storage (archival)

| Path | Purpose |
|---|---|
| `/mnt/biostore` | Long-term archival — NFS, slow, not for computation |
| `/mnt/cold02` | Cold storage — NFS, for data you rarely access |

These are managed separately from Lustre. Do not run jobs from these volumes. You can **copy** your data from any of these volumes to `/mnt/smart/scratch` as you need to process them. Don't forget to remove them right away when you don't need them anymore. 

---

## More

- [Transferring files to/from MARBITS](/docs/file-transfer/)
- [Backup policy](/docs/backup/)
- [FAQ — how to make symlinks](/docs/faq/#how-do-i-make-a-link-to-my-stuff-in-mntlustrebiousersmy-user-name)
