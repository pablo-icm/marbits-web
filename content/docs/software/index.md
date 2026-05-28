---
title: Software Environment
summary: How to discover, load, and manage software modules on MARBITS.
date: 2024-01-01
weight: 50
show_breadcrumb: true
---

{{< toc >}}

Software on MARBITS is managed via the **Environment Modules** (LMOD) system. Different versions of the same application can coexist and be loaded on demand, ensuring reproducibility across pipelines and projects. Environment modules allows us to keep co-existing versions of the same software, so you can use different versions, whether you want cross-compatibility with other datasets, you want to replicate an analysis or simply the newer version dropped some functionality that was vital for you. 

---

## LMOD

### List all software installed on MARBITS

```bash
module avail
```

When a program has more than one version, the default version that would be loaded when you don't specify any will show a `D` next to the app name.  

### Getting information about a module

```bash
# Show documentation, URL, special instructions
module help megahit/1.1.3

# One-line description
module whatis megahit/1.1.3
```

### Search for a specific tool

```bash
module spider blast
```

### Loading a module

```bash
module load <program>/<version>

# Example
module load megahit/1.1.3
```

Always make sure your SLURM scripts load **all required modules** after the `#SBATCH` header. If you don't specify the version, the default one will be loaded. Nevertheless, writing it down in your script will help you to document your process.

```bash
#!/bin/sh
#SBATCH --account=myproject
# ... other options ...

module load megahit/1.1.3
module load samtools/1.15

# your commands here
```

Once loaded, the executables and man pages are added to your `$PATH` automatically. You can call the program as if it were installed globally.


### Listing loaded modules

```bash
module list
```

### Unloading modules

```bash
# Unload a specific module
module unload megahit/1.1.3

# Unload all loaded modules
module purge
```

---


## Requesting new software

If you need a piece of software that is not yet available:

1. First check whether you can **install it in your home directory** or in your directory in `/mnt/smart/scratch`. Many Python/R packages or conda environments can be self-managed.

2. Otherwise, open a [GitHub Issue](https://github.com/marbits-icm/marbits-public/issues/new) requesting the software. Provide:
   - Tool name and version
   - URL / installation instructions
   - Why you need it (project context)

Admins will build a module and notify you.


---

## Conda / Mamba

Many users manage their own software environments with [conda](https://docs.conda.io/) or [mamba](https://mamba.readthedocs.io/). This is a supported workflow. Install miniconda/mambaforge in your Lustre user directory and manage environments there.

```bash
# Install mambaforge (example — check for the latest version)
wget https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
bash Mambaforge-Linux-x86_64.sh -p /mnt/smart/scratch/groupName/<username>/mambaforge

# Then load your env in your SLURM script
source /mnt/smart/scratch/groupName/<username>/mambaforge/etc/profile.d/conda.sh
conda activate myenv
```

---

## Containers (Docker, singularity, charliecloud...)

Very interesting, but not available at the moment. Docker looks like will never be available in Marbits. We are checking on other solutions. 

---

## Graphical user interface apps (GUI)

Not going to happen in Marbits.  
Yes, that includes Rstudio Server.  
There's an initiative to build some virtual machines in some server, but not at the moment. 

