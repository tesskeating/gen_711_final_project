# gen_711_final_project
Tess Keating
# Fecal Microbiota Transplant (FMT) Qiime2 Analysis
<details>

<summary>

## Background

</summary>

In a [human microbiome study](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-016-0225-7) by Kang et al., children with autism and gastrointestinal disorders were treated with fecal microbiota transplants to reduce their symptoms. For eighteen weeks, their microbiomes and severity of their symptoms were weekly monitored through fecal swab and stool samples. Using sequenced data from this study and a [Qiime2 tutorial](https://docs.qiime2.org/2024.2/tutorials/fmt/), a bioinformatic pathway analysis was performed. In this analysis, raw reads were denoised, sequences were aligned and classified, and phylogenies and diversity metrics were assessed. These bioinformatic techniques were used to generate results in the form of representative figures and visualizations.

</details>

<details>

<summary>

## Methods

</summary>

<details>

<summary>

### Obtaining, Denoising, and Merging Data

</summary>

Qiime Comands:

- *wget*: obtains initial data files (sample metadata and 10% subsample data)
- *demux summarize*: plots sequence quality to assess reads before denoising
###
- *dada2 denoise-single*: denoises sequences (removes errors and increases accuracy)
- *metadata tabulate*: tabulates denoised stats (amount of filtered, denoised, and non-chimeric read inputs)
- *feature-table tabulate-seqs*: gives sequence lengths
###
- *feature-table merge*: combines two feature tables
- *feature-table merge-seqs*: combines two groups of sequences
- *feature-table summarize*: tabulates and plots frequency stats
- *feature-table tabulate-seqs*: gives merged table with sequence lengths of each feature

<details>

<summary>Script:</summary>

</details>

</details>

</details>

<details>

<summary>

## Results

</summary>
