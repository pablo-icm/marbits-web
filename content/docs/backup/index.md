---
title: Backup
summary: Data backup policy on MARBITS and recommendations for protecting your work.
date: 2024-01-01
weight: 70
show_breadcrumb: true
---

{{< toc >}}

{{% callout warning %}}
**MARBITS does not guarantee data recovery.** Users are ultimately responsible for backing up data that is irreplaceable. Read this page to understand what is (and isn't) protected.
{{% /callout %}}

---

## What is backed up

| Location | Backed up? | Notes |
|---|---|---|
| `/home/<username>` | ✅ Nightly | Backed up because it lives on Lustre |
| `/mnt/lustre/bio/users/<username>` | ✅ Nightly | Your main user directory |
| `/mnt/lustre/repos` | ✅ Nightly | Public dataset repository |
| `/mnt/lustre/scratch` | ❌ **No** | Temporary — deleted after 3 months |
| `/mnt/smart` | ⚠ Limited | Currently the preferred workspace; limited backup |
| `/mnt/biostore` | ❌ No | Archival NFS — no automatic backup |
| `/mnt/cold02` | ❌ No | Cold storage — no automatic backup |

---

## Scratch auto-deletion

Files in `/mnt/lustre/scratch` that are older than **3 months** are automatically deleted. There is no warning. Always move finished job output to your permanent user directory:

```bash
mv /mnt/lustre/scratch/myrun/ /mnt/lustre/bio/users/<username>/myrun/
```

Since both paths are on the same Lustre filesystem, the `mv` is instantaneous — no data is actually copied.

---

## Recommendations

### 3-2-1 rule

For data you cannot afford to lose:

- Keep **3 copies** of important data
- On **2 different media** (e.g. Lustre + external drive or institutional storage)
- With **1 copy offsite** (e.g. cloud storage, your institute's backup service)

### Practical tips

1. **Keep raw data untouched** — never modify original files. Work on copies or use symbolic links.
2. **Compress everything** — `gzip`, `bzip2`, or `zstd` can reduce storage 3–10×.
3. **Document your workflows** — a reproducible pipeline is almost as good as a backup.
4. **Use version control** — for scripts, analysis code, and configuration files, use `git`.
5. **Delete intermediates** — derived files that can be regenerated don't need to be backed up.

### For large original datasets

If you have large datasets that were downloaded from public repositories (NCBI, ENA, etc.), ask the admins to place them in `/mnt/lustre/repos`. This is the read-only repository for data that can be re-downloaded, saving space in your personal quota.

---

## Contact

Data-related questions: open an [Issue](https://github.com/marbits-icm/marbits-public/issues) or ask in [Discussions](https://github.com/marbits-icm/marbits-public/discussions).
