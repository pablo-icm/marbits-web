---
title: FAQ
summary: Frequently asked questions about using MARBITS.
date: 2024-01-01
weight: 80
show_breadcrumb: true
---

{{< toc >}}

---

## How do I cite MARBITS in my scientific work?

It is important to give visibility to the bioinformatics platform in papers, posters and presentations. Please cite it as:

> *High-Performance computing analyses were run at the Marine Bioinformatics Service (MARBITS) of the Institut de Ciències del Mar (ICM-CSIC) in Barcelona.*

If you received direct help from a team member who is not an author, please also add:

> *We thank Pablo S. / Vane B. / Ramiro L. for his/her help to run multiple/specific bioinformatics analyses.*

We also have a **logo** you can include in slides — ask the admins.

---

## How do I request a user account?

Send an email to [psanchez@icm.csic.es](mailto:psanchez@icm.csic.es) with:
- Your name and institution
- Your supervisor's name
- The project/bank account(s) your compute time should be billed to

---

## How can I access MARBITS from outside the local network?

1. Log in to the `triton` gateway server (ask IT if you need an account):
   ```bash
   ssh <triton_username>@triton.cmima.csic.es
   ```
2. From `triton`, SSH into MARBITS:
   ```bash
   ssh <marbits_username>@marbits.cmima.csic.es
   ```

For file transfers from outside, see [File Transfer](/docs/file-transfer/).

---

## How do I know my "bank" account for `--account`?

You probably have only one bank account, which is also your default — so you often don't need to specify it at all. To list all accounts associated to your user:

```bash
sacctmgr show assoc user=<your_username>
```

---

## How do I make a symlink to my Lustre data in my home?

Your `/home` is tiny. Keep your data in Lustre and create symlinks for convenience:

```bash
ln -s /mnt/lustre/bio/users/<username>/myproject ~/myproject
```

The symlink behaves exactly like a directory — you can `cd` into it, list it, etc.

---

## How can I transfer files between my local machine and MARBITS?

See the full [File Transfer](/docs/file-transfer/) page. Quick summary:

```bash
# From inside CMIMA network
rsync -avz --progress myfile <username>@marbits:/mnt/lustre/bio/users/<username>/

# From outside (via SSH tunnel on port 2222)
rsync -avz -e "ssh -p 2222" --progress myfile <username>@localhost:/mnt/lustre/bio/users/<username>/
```

---

## My job dies immediately and I'm sure the software and files are correct. What's wrong?

Are you trying to run it directly on the login node (`marbits`)? **Don't.** Processes that use too many resources on the head node are killed automatically.

Submit your job with `sbatch` or start an interactive session with `srun --pty /bin/bash`. See [Running Jobs](/docs/running-jobs/).

---

## I have several open sessions on MARBITS but only one terminal. What are those?

If `who` or `w` shows multiple sessions for your user that you are not currently in, they are zombie sessions left from closed terminal windows or screensaver lockouts. The system will eventually clean them up, but you can do it manually:

```bash
who          # note the pts/NUMBER of the unwanted session
pkill -9 -t pts/NUMBER
```

---

## Where do I report bugs or request new software?

Open an [Issue](https://github.com/marbits-icm/marbits-public/issues/new) on GitHub. For general questions and discussion, use the [Discussions](https://github.com/marbits-icm/marbits-public/discussions) forum.

---

## I was a biocluster user. Where is my data?

If you had an account on the old biocluster (SGE-based) before the upgrade to MARBITS/SLURM, your data should have been migrated to the Lustre filesystem under `/mnt/lustre/bio/users/<username>`.

Main changes from biocluster to MARBITS:
- Job submission: `qsub` (SGE) → `sbatch` (SLURM)
- Storage: NFS → Lustre parallel filesystem
- Cluster software: Rocks v6 → OpenHPC v1.3.4

---

## How do I add a GitHub user to the MARBITS community?

Post your GitHub username in [this discussion thread](https://github.com/marbits-icm/marbits-public/discussions/6). Having a GitHub account lets you participate in discussions, open issues, and contribute to the wiki.
