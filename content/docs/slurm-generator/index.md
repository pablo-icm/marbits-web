---
title: SLURM Script Generator
summary: Interactive generator for SLURM job script headers — fill in the form and get a ready-to-use #SBATCH block.
date: 2024-01-01
weight: 45
show_breadcrumb: true
---

Fill in the parameters below and the `#SBATCH` header will be generated in real time on the right. Click **Copy** to paste it into your script.

{{< slurm-generator >}}

---

## Quick reference

| Option | Description |
|--------|-------------|
| `--account` | Billing account (required). Check yours with `sacctmgr show user $(whoami)`. |
| `--job-name` | Appears in `squeue` output. Use short, descriptive names. |
| `--nodes` | Number of compute nodes. Use `1` unless running MPI across nodes. |
| `--ntasks` | Total MPI tasks. For serial/threaded jobs keep this at `1`. |
| `--cpus-per-task` | Threads per task. Must match `--threads` / `-t` of your program. |
| `--mem` | RAM per node. Suffix `M` (MB), `G` (GB), `T` (TB). |
| `--time` | Wall-clock limit. Job is killed when reached. Format: `D-HH:MM:SS`. |
| `--output` | Path for stdout. `%x` = job name, `%j` = job ID. |
| `--error` | Path for stderr. Same substitutions available. |
| `--array` | Submit many similar jobs at once. `%a` in filenames = array index. |

{{% callout note %}}
Always create the `logs/` directory before submitting:
```bash
mkdir -p logs
sbatch job.sh
```
{{% /callout %}}

See [Running Jobs](/docs/running-jobs/) for full examples and job monitoring commands.
