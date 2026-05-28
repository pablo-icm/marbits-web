---
title: File Transfer
summary: How to copy files between your local computer and MARBITS using rsync, scp, or an FTP client.
date: 2024-01-01
weight: 60
show_breadcrumb: true
---

{{< toc >}}

There are several ways to move files between your local machine and MARBITS. Choose the method that works best for you.

---

## From inside the CMIMA network

### Command line: `rsync` or `scp`

Both tools work from within the CMIMA local network. Run the commands **from your local computer**:

```bash
# Using rsync (preferred — resumes interrupted transfers)
rsync -avz --progress <local_file> <username>@marbits:/path/on/marbits/

# Using scp
scp <local_file> <username>@marbits:/path/on/marbits/

# Copying a whole directory
rsync -avz --progress my_data/ <username>@marbits:/mnt/lustre/bio/users/<username>/my_data/
```

To copy from MARBITS to your local machine:

```bash
rsync -avz --progress <username>@marbits:/mnt/lustre/bio/users/<username>/results/ ./results/
```

### Graphical client: Cyberduck / FileZilla

Use any **SFTP** client (not regular FTP):

| Setting | Value |
|---|---|
| Protocol | **SFTP** (SSH File Transfer Protocol) |
| Server | `marbits` |
| Port | `22` |
| Username | Your MARBITS username |
| Password | Your MARBITS password |

Recommended clients:
- **[Cyberduck](https://cyberduck.io/)** — macOS / Windows, free-ish
- **[FileZilla](https://filezilla-project.org/)** — macOS / Linux / Windows, free

---

## From outside the CMIMA network

### VPN
You are good to go. See above.  

### Through `salamandra` 

You must first establish an **SSH tunnel** through the `salamandra` gateway.

#### Open the tunnel

From your local computer:

```bash
ssh -L 2222:marbits:22 <salamandra_username>@salamandra.cmima.csic.es
```

Leave this terminal open (the tunnel is active as long as it runs).

#### Transfer files via tunnel

In another terminal, use `localhost:2222` as the target:

```bash
# rsync through tunnel
rsync -avz -e "ssh -p 2222" --progress <local_file> <marbits_username>@localhost:/mnt/lustre/bio/users/<marbits_username>/

# scp through tunnel
scp -P 2222 <local_file> <marbits_username>@localhost:/path/on/marbits/
```

### Graphical client via tunnel

Configure your FTP client as follows:

| Setting | Value |
|---|---|
| Protocol | **SFTP** |
| Server | `localhost` |
| Port | `2222` |
| Username | Your **MARBITS** username (not `salamandra`'s') |
| Password | Your **MARBITS** password |

---

## Tips for large transfers

- Prefer `rsync` over `scp` for large datasets — it resumes interrupted transfers.
- Compress files before transferring when possible (`tar -czf archive.tar.gz my_data/`).
- For very large datasets (>1 TB), contact the admins — there may be a faster option.
