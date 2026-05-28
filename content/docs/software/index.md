---
title: Software Environment
summary: How to discover, load, and manage software modules on MARBITS.
date: 2024-01-01
weight: 50
show_breadcrumb: true
---

{{< toc >}}

Software on MARBITS is managed via the **Environment Modules** system. Different versions of the same application can coexist and be loaded on demand, ensuring reproducibility across pipelines and projects.

---

## Discovering available software

List all software installed on MARBITS:

```bash
module avail
```

Search for a specific tool (e.g. `blast`):

```bash
module avail blast
```

---

## Loading a module

```bash
module load <program>/<version>

# Example
module load megahit/1.1.3
```

Once loaded, the executables and man pages are added to your `$PATH` automatically. You can call the program as if it were installed globally.

---

## Listing loaded modules

```bash
module list
```

Always make sure your SLURM scripts load **all required modules** after the `#SBATCH` header:

```bash
#!/bin/sh
#SBATCH --account=myproject
# ... other options ...

module load megahit/1.1.3
module load samtools/1.15

# your commands here
```

---

## Unloading modules

```bash
# Unload a specific module
module unload megahit/1.1.3

# Unload all loaded modules
module purge
```

---

## Getting information about a module

```bash
# Show documentation, URL, special instructions
module help megahit/1.1.3

# One-line description
module whatis megahit/1.1.3
```

---

## Requesting new software

If you need a piece of software that is not yet available:

1. First check whether you can **install it in your home directory** (remember: 5 GB quota!). Many Python/R packages or conda environments can be self-managed.

2. Otherwise, open a [GitHub Issue](https://github.com/marbits-icm/marbits-public/issues/new) requesting the software. Provide:
   - Tool name and version
   - URL / installation instructions
   - Why you need it (project context)

Admins will build a module and notify you.

{{% callout note %}}
Home-made scripts and personal conda environments are fine — just install them in your Lustre user directory (`/mnt/lustre/bio/users/<username>`) to avoid filling up your `/home` quota.
{{% /callout %}}

---

## Conda / Mamba

Many users manage their own software environments with [conda](https://docs.conda.io/) or [mamba](https://mamba.readthedocs.io/). This is a supported workflow. Install miniconda/mambaforge in your Lustre user directory and manage environments there.

```bash
# Install mambaforge (example — check for the latest version)
wget https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
bash Mambaforge-Linux-x86_64.sh -p /mnt/lustre/bio/users/<username>/mambaforge

# Then load your env in your SLURM script
source /mnt/lustre/bio/users/<username>/mambaforge/etc/profile.d/conda.sh
conda activate myenv
```
