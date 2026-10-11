# CIPA, part two: what happens to the cells that should feel pain?

My last project in this series asked whether a model could tell pathogenic NTRK1 variants from benign ones. This one asks a different question: what do the cells that actually carry NTRK1 look like, and what happens to the nervous system's pain-sensing machinery when that gene fails?

## What I did

I used human dorsal root ganglion (DRG) single-nucleus RNA-seq data from six donors (Nguyen et al. 2021, eLife), 1837 nuclei after quality filtering. DRG neurons are the cell bodies of the sensory neurons that carry pain, touch, and temperature signals from the body to the spinal cord, this is the actual tissue where CIPA does its damage.

I clustered the cells, looked for NTRK1 expression, and ran into something I didn't expect: several of my clusters were almost entirely made up of cells from a single donor. With only six donors and a few hundred cells each, the clustering was picking up batch effects alongside real biology, and I wasn't going to pretend otherwise.

## What I found

Rather than trust cluster identity alone, I checked whether the core biological signal held up within each donor separately, not just in the pooled data.

It did. **NTRK1 and GFRA2 expression are anti-correlated in every single one of the six donors independently** (correlations ranging from -0.06 to -0.26, all negative). These two genes mark the two classic branches of nociceptor (pain neuron) in the DRG:

- **NTRK1 (TrkA)** marks peptidergic nociceptors, the neurons that release CGRP and express TRPV1 and SCN10A (Nav1.8)
- **GFRA2 (Ret co-receptor)** marks the separate non-peptidergic nociceptor lineage

These two programs are largely mutually exclusive at the single-cell level, and that split shows up consistently across every donor in this dataset, not just when the data is pooled together. This is the molecular architecture CIPA disrupts: when NTRK1 fails, it isn't just "a gene," it's the identity marker and survival signal for an entire functional class of pain-sensing neuron.

## A note on the batch effect

I'm including this because it's the more honest and, I think, more useful part of the project. With 14 Leiden clusters spread across only six donors, several clusters turned out to be 95-100% single-donor, a clear sign of batch effect dominating over biology at this sample size. Rather than report cluster-level findings as if they were clean, I validated the one finding that held, the NTRK1/GFRA2 split, at the donor level directly. Small single-cell datasets are genuinely useful, but only if you check whether what you're seeing is biology or a donor artifact before you report it.

## Repo structure
notebooks/ # Colab notebook: loading, QC, clustering, marker genes, validation
data/ # Raw sample CSVs (Nguyen et al. 2021, GSE168243)
results/ # Marker gene table, donor correlation table, final figure

## Data source

Nguyen MQ, von Buchholtz LJ, Reker AN, Ryba NJF, Davidson S. "Single-nucleus transcriptomic analysis of human dorsal root ganglion neurons." eLife, 2021. [GSE168243](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE168243)

## Series so far

1. [NTRK1 variant pathogenicity classifier](https://github.com/Bioinformatician0507/cipa-ntrk1-variants)
2. This project

---
Iqra Nadeem | [LinkedIn](https://linkedin.com/in/iqra-nadeem) | [GitHub](https://github.com/Bioinformatician0507)
