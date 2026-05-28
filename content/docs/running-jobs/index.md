---
title: Running Jobs
summary: How to submit and manage jobs with the SLURM workload manager.
date: 2024-01-01
weight: 40
show_breadcrumb: true
---

{{< toc >}}

MARBITS uses [**SLURM**](https://slurm.schedmd.com/overview.html) as its workload manager. SLURM allocates resources across nodes, launches your jobs, and ensures fair sharing between users.

{{% callout warning %}}
**Never run analyses on the login node (`marbits`).** Always submit work through SLURM. Processes that consume too many resources on the head node will be killed without warning.
{{% /callout %}}

---

## Basic submission

The standard way to run a job is to write a **batch script** and submit it with `sbatch`:

```bash
sbatch my_script.sh
```

---

## SLURM options

All SLURM options are placed at the top of your script, preceded by `#SBATCH`. They look like comments to the shell but SLURM reads them.

### Required option

```bash
#SBATCH --account=<your_bank_account>
```

Every job must be billed to a bank/project account. One user may belong to several accounts. See [how to find your bank account](/docs/faq/#how-do-i-know-my-bank-account-for-option-account).

### Recommended options

```bash
#SBATCH --job-name=<name>           # Human-readable job name
#SBATCH --time=DD-HH:MM:SS          # Walltime limit (job killed if exceeded)
#SBATCH --mem=<MB>                  # Memory per node (e.g. 10G, 512M)
#SBATCH --ntasks=1                  # Number of tasks (usually 1)
#SBATCH --cpus-per-task=<N>         # Cores per task
#SBATCH --nodes=<N>                 # Number of nodes (omit unless using MPI/arrays)
#SBATCH --output=logs/job_%J.out    # Stdout log (%J = job ID)
#SBATCH --error=logs/job_%J.err     # Stderr log
#SBATCH --mail-type=ALL             # Email notifications (BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=you@icm.csic.es
#SBATCH --array=1-10                # Job array (see below)
```

{{% callout note %}}
`--cpus-per-task` must match the number of threads your program actually uses. If you request 12 cores but your program only uses 1, you waste 11 cores.
{{% /callout %}}

---

## Example: single-core job

```bash
#!/bin/sh
#SBATCH --account=myproject
#SBATCH --job-name=megahit_assembly
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=12G
#SBATCH --time=0-04:00:00
#SBATCH --output=logs/megahit_%J.out
#SBATCH --error=logs/megahit_%J.err
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=psanchez@icm.csic.es

module load megahit/1.1.3

reads1=data/sample_R1.fastq.gz
reads2=data/sample_R2.fastq.gz
outdir=/mnt/lustre/scratch/psanchez/megahit_out

megahit -o ${outdir} --out-prefix assembly -1 ${reads1} -2 ${reads2}
```

---

## Example: multi-core job

The key point: **`--cpus-per-task` must equal the number of threads you pass to the program.**

```bash
#!/bin/sh
#SBATCH --account=myproject
#SBATCH --job-name=megahit_12t
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=12          # ← must match -t below
#SBATCH --mem=24G
#SBATCH --time=0-08:00:00
#SBATCH --output=logs/megahit_%J.out
#SBATCH --error=logs/megahit_%J.err

module load megahit/1.1.3

megahit -t 12 -o /mnt/lustre/scratch/psanchez/out \  # ← must match --cpus-per-task
        -1 data/R1.fastq.gz -2 data/R2.fastq.gz
```

---

## Example: job array

Job arrays are ideal when you have many similar input files to process. SLURM creates one sub-job per index value, each with its own `$SLURM_ARRAY_TASK_ID`.

```bash
# If your input files are named infile1.fasta, infile2.fasta, infile3.fasta
#!/bin/sh
#SBATCH --account=myproject
#SBATCH --job-name=count_seqs
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=1G
#SBATCH --output=logs/count_%A_%a.out   # %A = array job ID, %a = array index
#SBATCH --error=logs/count_%A_%a.err
#SBATCH --array=1-3%1                   # indices 1-3, max 1 running at a time

grep -c '^>' infile${SLURM_ARRAY_TASK_ID}.fasta > infile${SLURM_ARRAY_TASK_ID}.count.txt
```

- `--array=1-10%2` runs indices 1-10 with **at most 2 jobs running simultaneously**.
- For large arrays with many tasks, add `--exclusive=user` to prevent spreading across the whole cluster.

---

## Interactive sessions

To get an interactive shell on a compute node:

```bash
# Minimal interactive session (1 core, default memory)
srun --pty /bin/bash

# 4 cores, 10 GB RAM
srun -A myproject -c 4 --mem=10G --pty /bin/bash

# Exit when done
exit   # or Ctrl+D
```

{{% callout note %}}
`--pty` is required — without it you will not get an interactive prompt.
{{% /callout %}}

---

## Modifying running jobs

Use `scontrol update` to change options on already-submitted jobs:

```bash
# Change array throttle (number of simultaneous tasks)
scontrol update JobId=<ID> ArrayTaskThrottle=10
scontrol update JobName=<name> ArrayTaskThrottle=10

# Change memory allocation
scontrol update JobName=<name> MinMemoryNode=<MB>
```

---

## Monitoring and accounting

### Check the queue

```bash
squeue          # all jobs
squeue -u $(whoami)   # your jobs only
```

### Check node status

```bash
sinfo
```

### Cancel jobs

```bash
scancel <jobID>            # cancel by ID
scancel -n <jobname>       # cancel by name
scancel -u $(whoami)       # cancel all your jobs
```

### Accounting for finished jobs

```bash
sacct                      # recent jobs
sacct -j <jobID>           # specific job details
```

### Monitor a running job

```bash
scontrol show job <jobID>
```

---

## Useful aliases

Add these to your `~/.bashrc` for friendlier output:

```bash
# SLURM aliases
alias sq="squeue -o \"%10A %12j %5K %10u %8a %10P %3t %10M %6D %6C %10f %R\" -u $(whoami)"
alias sqa="squeue -ao \"%10A %12j %5K %10u %8a %10P %3t %10M %6D %6C %10f %R\""
alias si="sinfo -o \"%14R %10n %5a %7t %6c %8O %8m %8e %7z %60E\""
alias sacct="sacct --format=jobid,jobname,submit,start,end,elapsed,ncpus,ntasks,MaxVMSize,AllocNodes,state"
```

---

## Benchmarking your jobs

Before hardcoding memory and time values, run a test job and check actual usage:

```bash
sacct -j <jobID>   # shows elapsed time, MaxVMSize, etc.
```

Accurate resource requests help SLURM schedule everyone more efficiently and give you better "fair-share karma" (priority for future jobs).
