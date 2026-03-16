# arctic-wolf-population-genomics

> Population genomic analysis of Arctic wolf (*Canis lupus arctos*) across High Arctic island populations and mainland North America.

---

## Overview

This repository contains the full analysis pipeline, scripts, and results for a population genomics study of Arctic wolves. Using genome-wide SNP data, we characterise genetic structure across four High Arctic island populations and mainland wolves, finding evidence for **island-level genetic structuring** rather than a single panmictic Arctic population or a simple Arctic–mainland divide.

### Study populations

| Population | Region |
|---|---|
| Ellesmere Island | Canadian High Arctic |
| Baffin Island | Canadian Arctic Archipelago |
| Banks Island | Western Canadian Arctic |
| Greenland | Northeast Greenland |
| Mainland | Northern & central North America |

---

## Hypotheses

Three competing hypotheses were evaluated:

- **H1** — A genetically distinct Arctic wolf population exists relative to mainland North American wolves
- **H2** — Arctic wolves form a single panmictic population with no island-level structure
- **H3** ✓ — Arctic island populations represent genetically distinct units relative to each other and to mainland wolves

Results support **H3**: inter-island FST values are comparable to island–mainland FST values, ADMIXTURE recovers K=5 island-specific ancestry components, and island populations do not cluster together in PCA.

---

## Repository structure

```
arctic-wolf-population-genomics/
├── data/
│   ├── raw/                  # Raw genotype files (VCF)
│   ├── filtered/             # Post-QC SNP datasets
│   └── metadata/             # Sample information, coordinates
├── scripts/
│   ├── 01_qc_filtering.sh    # SNP filtering, MAF, LD pruning
│   ├── 02_pca.sh             # PCA with PLINK
│   ├── 03_admixture.sh       # ADMIXTURE K=1–10, CV error
│   ├── 04_fst.sh             # Pairwise FST (vcftools)
│   ├── 05_diversity.sh       # Nucleotide diversity π per population
│   └── 06_phylogeny.sh       # Phylogenetic tree (IQ-TREE2)
├── results/
│   ├── pca/                  # PCA plots and eigenvalues
│   ├── admixture/            # Bar plots, CV error curves
│   ├── fst/                  # Pairwise FST matrix
│   ├── diversity/            # π estimates per population
│   └── phylogeny/            # Tree files and figures
├── figures/                  # Publication-ready figures
├── docs/                     # Methods notes and references
└── README.md
```

---

## Analysis pipeline

Analyses are run in the following order, each step informed by the previous:

### 1. Quality control & filtering
- SNP filtering (missingness, MAF threshold)
- LD pruning
- Outlier sample removal

### 2. PCA
- Tool: `PLINK v1.9`
- Visualises broad genetic structure without model assumptions
- Identifies whether island samples cluster together or separately

### 3. ADMIXTURE
- Tool: `ADMIXTURE v1.3`
- K=1–10 tested; best K selected by cross-validation (CV) error
- Run with and without mainland samples
- Identifies ancestry components per population

### 4. FST
- Tool: `VCFtools`
- Pairwise FST calculated between all population pairs
- Key comparison: inter-island FST vs island–mainland FST

### 5. Nucleotide diversity (π)
- Tool: `VCFtools` / `pixy`
- Per-population π calculated in sliding windows
- Compared between island and mainland populations

### 6. Phylogenetic tree
- Tool: `IQ-TREE2`
- Maximum-likelihood tree from genome-wide SNPs
- Rooted with outgroup (*Canis latrans* or domestic dog)
- Tests whether islands form independent branches

---

## Dependencies

| Tool | Version | Use |
|---|---|---|
| PLINK | 1.9 | QC, PCA |
| ADMIXTURE | 1.3 | Ancestry estimation |
| VCFtools | 0.1.16 | FST, diversity |
| pixy | 1.2 | Nucleotide diversity |
| IQ-TREE2 | 2.2 | Phylogenetic inference |
| R | ≥ 4.0 | Visualisation |
| Python | ≥ 3.9 | Helper scripts |

R packages: `ggplot2`, `tidyverse`, `pophelper`

---

## Key results

- PCA: Island populations scatter in distinct directions; no shared Arctic cluster
- ADMIXTURE: K=5 best supported; each island carries a unique ancestry component with minimal inter-island admixture
- FST: Inter-island FST comparable to island–mainland FST; no lower divergence within Arctic islands
- Nucleotide diversity: Reduced π on island populations relative to mainland, consistent with founder effects and genetic drift
- Phylogeny: Island populations recovered as independent lineages

---

## Citation

> *To be added upon publication*

---

## Contact

> *To be added*

---

## License

This project is licensed under the MIT License — see `LICENSE` for details.
