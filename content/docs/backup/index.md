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

## Data Back-up policy

**There's no back-up**  

There used to be a tape back-up server. Not anymore. Scientific Computation Service is looking for options to bring it back.

## Recommendations

### 3-2-1 rule

For data you cannot afford to lose:

- Keep **3 copies** of important data
- On **2 different media** (e.g. Lustre + external drive or institutional storage)
- With **1 copy offsite** (e.g. cloud storage, your institute's backup service, an HDD under your matress)

### Practical tips

1. **Keep raw data untouched** — never modify original files. Work on copies or use symbolic links. Submit all raw data to the appropriate public repositories as soon as possible. Some repos allow files to be embargoed for quite some time.  
2. **Compress everything** — `gzip`, `bzip2`, or `zstd` can reduce storage 3–10×.
3. **Document your workflows** — a reproducible pipeline is almost as good as a backup.
4. **Use version control** — for scripts, analysis code, and configuration files, use `git`.
5. **Delete intermediates** — derived files that can be regenerated don't need to be backed up.

### Shared datasets

If you want to download public datasets that may be used by other users, ask the admins to place them in an accessible place. Let's try not to duplicate things now that we are short in storage space. 

---

## Contact

Data-related questions: open an [Issue](https://github.com/marbits-icm/marbits-public/issues) or ask in [Discussions](https://github.com/marbits-icm/marbits-public/discussions).
