---
title: Anvio interactive session via browser
summary: How to run an interactive Anvio session on a MARBITS compute node and view it in your local browser.
date: 2024-01-01
weight: 91
show_breadcrumb: true
authors:
  - "@ramalok"
  - "@flatorre"
---

*Tutorial by @ramalok and @flatorre.*

[Anvio](https://anvil.microbiome.tips/) is a powerful interactive platform for microbial 'omics, but it needs a web browser to display its interface. Since MARBITS compute nodes don't have a display, you'll need to set up an SSH tunnel to forward the browser port to your local machine.

---

## Step 1 — Start an interactive SLURM session

```bash
srun -A emm3 -c 4 --mem=20G --pty /bin/bash
```

Note which **node** SLURM assigns to you (e.g. `c05`). You'll need this in step 3.

---

## Step 2 — Run Anvio in server-only mode

Inside the interactive session, launch the Anvio process you want to visualise:

```bash
anvi-interactive \
    -p merged.profiles/PROFILE.db \
    -c contigs.db \
    -C myMAGs \
    -P 8787 \
    --server-only
```

- `-P 8787` — sets the port Anvio listens on
- `--server-only` — prevents Anvio from trying to open a local browser (which would fail on the cluster)

Leave this running.

---

## Step 3 — Create an SSH tunnel from your local computer

In a **new terminal on your local machine**, run:

```bash
ssh -t -t <username>@marbits -L 8787:localhost:8787 ssh c05 -L 8787:localhost:8787
```

Replace `c05` with the node name that SLURM gave you in step 1, and `<username>` with your MARBITS username.

This double-tunnel forwards port `8787` from your local machine → `marbits` login node → compute node `c05`.

---

## Step 4 — Open Anvio in your browser

Open your browser and go to:

```
http://localhost:8787
```

Anvio's interactive interface should appear. 🎉

---

## Notes

- Port `8787` is just an example — you can use any port not already in use.
- When you're done, close the browser, then exit the interactive session (`exit` or `Ctrl+D`), and close the SSH tunnel terminal.
- If the port is already in use, try `8788`, `9000`, etc.

---

## See also

- [DADA2 tutorial for MARBITS](https://github.com/adriaaula/dada2_guidelines) by @aauladell and @aleixop
- [Running Jobs](/docs/running-jobs/)
