---
title: One-liners and small scripts
summary: Useful command-line snippets and bioinformatics one-liners for common tasks.
date: 2024-01-01
weight: 92
show_breadcrumb: true
---

{{< toc >}}

A growing collection of short commands and scripts that solve common bioinformatics problems. Contribute yours by opening a [GitHub Issue](https://github.com/marbits-icm/marbits-public/issues)!

---

## FASTA manipulation

### Remove specific sequences from a FASTA file

If you want to remove sequences by ID from a large FASTA file, `samtools faidx` + reverse-listing works, but for very large files this efficient `awk` one-liner is faster:

```awk
awk 'BEGIN{while((getline < "seqsToDelete.ffn")>0)l[">"$1]=1}/^>/{f=!l[$1]}f' seqs.ffn
```

- `seqsToDelete.ffn` — a plain text file with one sequence ID per line (no `>` needed)
- `seqs.ffn` — your input FASTA file
- Output goes to stdout; redirect with `> filtered.ffn`

**Alternative with `seqkit`** (if the module is available):

```bash
module load seqkit
seqkit grep -v -f seqsToDelete.txt seqs.fna > filtered.fna
```

---

## More one-liners coming soon

Have something useful? Add it by opening an [Issue](https://github.com/marbits-icm/marbits-public/issues/new) or submitting a pull request to the wiki.

---

## External resources

- [The Biostar Handbook](https://www.biostarhandbook.com/) — bioinformatics recipes
- [Bioinformatics one-liners (GitHub)](https://github.com/stephenturner/oneliners) — large curated collection
- [Rosalind](https://rosalind.info/) — bioinformatics programming problems
