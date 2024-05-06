# gen_711_final_project

# Fecal Microbiota Transplant (FMT) Qiime2 Analysis

Tess Keating

<details>

<summary>

## Background

</summary>

In a [human microbiome study](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-016-0225-7) by Kang et al., children with autism and gastrointestinal disorders were treated with fecal microbiota transplants to reduce their symptoms. For eighteen weeks, their microbiomes and severity of their symptoms were monitored through fecal swab and stool samples. Using sequenced data from this study and a [Qiime2 tutorial](https://docs.qiime2.org/2024.2/tutorials/fmt/), a bioinformatic pathway analysis was performed. In this analysis, raw reads were denoised and merged, sequences were aligned and classified, phylogenies were created, and diversity metrics were assessed. These bioinformatic techniques were used to generate results in the form of representative figures and visualizations.

</details>

<details>

<summary>

## Methods

</summary>

My [full script](https://github.com/tesskeating/gen_711_final_project/blob/main/finalprojectscript.txt) contains all commands that I used for this project. It is organized into the same headers that I used below. Under each header below is a discription of each command.

<details>

<summary>

### 1. Obtaining, Denoising, and Merging Data

</summary>

**Qiime Commands:**

[source for commands below](https://docs.qiime2.org/2024.2/tutorials/fmt/):

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
- *feature-table tabulate-seqs*: makes merged table with sequence lengths of each feature

</details>

<details>

<summary>

### 2. Aligning Sequences

</summary>

**Qiime Commands:**

[source for commands below](https://docs.qiime2.org/2022.2/tutorials/phylogeny/#sequence-alignment):

- *alignment mafft*: aligns sequences of feature table
- *alignment mask*: removes ambiguous positions from alignment

</details>

<details>

<summary>

### 3. Classifying Sequences

</summary>

**Qiime Commands:**

[source for classifier](https://zenodo.org/records/6395539#.ZGE7pHbMJhE)

[source for commands below](https://docs.qiime2.org/2024.2/tutorials/feature-classifier/):

- *wget*: obtains 16s rRNA human stool classifier (not included in repo because file was too big to push)
- *feature-classifier classify-sklearn*: assigns taxonomy to rep sequences
- *metadata tabulate*: tabulates taxon and confidence of each feature

</details>

<details>

<summary>

### 4. Making Phylogenetic Tree

</summary>

**Qiime Commands:**

[source for commands below](https://docs.qiime2.org/2024.2/tutorials/phylogeny/#fasttree):

- *phylogeny fasttree*: makes tree from aligned sequences
- *phylogeny midpoint-root*: roots tree

[source for getting empress](https://library.qiime2.org/plugins/empress/32/)

[source for commands below](https://github.com/biocore/empress#tutorial-using-empress-in-qiime-2):

- *empress tree-plot*: adds taxa to rooted tree
- *empress community-plot*: plots phylogenies and taxonomic community data

</details>

<details>

<summary>

### 5. Assessing Diversity Metrics

</summary>

**Qiime Commands:**

[source for command below](https://docs.qiime2.org/2024.2/tutorials/filtering/):

- *feature-table filter-samples*: filters samples to compare control and treatment groups

[source for command below](https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/040-even-sampling.html):

- *feature-table summarize*: makes filtered table to determine sequence depth

[source for command below](https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/050-core-metrics.html):

- *diversity core-metrics-phylogenetic*: makes and plots alpha and beta diversity metrics using sequence depth

[source for command below](https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/040-even-sampling.html):

- *diversity alpha-rarefaction*: verifies sequence depth and plots depth vs diversity

[source for commands below](https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/060-alpha-diversity.html):

- *diversity alpha-group-significance*: plots alpha diversity vs observed features
- *longitudinal linear-mixed-effects*: makes alpha diversity linear plot with weekly treatment vs diversity

[source for commands below](https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/070-beta-diversity.html):

- *diversity umap*: reduces dimensions of beta diversity metrics using unweighted and weighted unifrac matrices
- *metadata tabulate*: tabulates unifrac matrices using diversity values (Faith's phylogenetic diversity, evenness, and Shannon diversity)
- *taxa barplot*: makes taxonomy barplot
- *emperor plot*: plots umap and pcoa data from beta diversity unifrac matrices

[source for commands below](https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/080-longitudinal.html):

- *taxa collapse*: adds taxa to feature table
- *feature-table filter-features-conditionally*: filters abundance of genera in feature table
- *feature-table relative-frequency*: converts counts in filtered feature table to relative frequencies
- *longitudinal volatility*: makes longitudinal volatility plot using metadata, diversity metrics, and taxa and relative frequencies from table
- *longitudinal feature-volatility*: makes volatility control plot to identify features that change over time

</details>

<details>

<summary>

### Other Notes

</summary>

- *git clone*: clones github repo into new directory
- *git add*: adds all directories and files in project directory
- *git commit*: saves changes to local repo
- *git push*: uploads content in local repo to github repo
###
I downloaded any qzv files that I wanted to view to my desktop and [uploaded to Qiime](https://view.qiime2.org/).

</details>

</details>

<details>

<summary>

## Results

</summary>

Below are examples of visualizations that can be generated from each of the 5 methods above.

<details>

<summary>

### Obtaining, Denoising, and Merging Data Visualizations

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/7c1d8399-e463-4395-a55e-dcf27d783cb6)

This is
