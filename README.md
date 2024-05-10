# gen_711_final_project

# Fecal Microbiota Transplant (FMT) Qiime2 Analysis

Tess Keating

<details>

<summary>

## Background

</summary>

In a [human microbiome study](https://microbiomejournal.biomedcentral.com/articles/10.1186/s40168-016-0225-7) by Kang et al., children with autism and gastrointestinal disorders were treated with fecal microbiota transplants to reduce their symptoms. For 18 weeks, their microbiomes and severity of their symptoms were monitored through fecal swab and stool samples. Using sequenced data from this study and a [Qiime2 tutorial](https://docs.qiime2.org/2024.2/tutorials/fmt/), a bioinformatic pathway analysis was performed. In this analysis, raw reads were denoised and merged, sequences were aligned and classified, phylogenies were created, and diversity metrics were assessed. These bioinformatic techniques were used to generate results in the form of representative figures and visualizations.

</details>

<details>

<summary>

## Methods

</summary>

My [full script](https://github.com/tesskeating/gen_711_final_project/blob/main/finalprojectscript.txt) contains all commands that I used for this project. It is organized into the same headers that I used below. Under each header below is a discription of each command. All commands were run on my laptop using vscode.

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

- *wget*: obtains 16s rRNA human stool classifier from silva database (not included in repo because file was too big to push)
- *feature-classifier classify-sklearn*: assigns taxonomy to rep sequences
- *metadata tabulate*: tabulates taxa and confidence of each feature

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

Below are examples of visualizations that can be generated using the methods in the previous section.

<details>

<summary>

### Sequence Quality and Features Visualizations

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/7c1d8399-e463-4395-a55e-dcf27d783cb6)

This histogram shows the sequence quality of each forward read input. It helps determine the minimum sequence quality prior to denoising, which filters the sequences and removes reads that have too much noise. In this case, the minimum demultiplexed sequence count is 1208.

command used: *demux summarize* from Obtaining, Denoising, and Merging Data

<br/>

<br/>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/46ef71eb-d93e-41a8-9af3-81d8b7dc5eb0)

This is part of a merged table with each feature's sequence and sequence length. It shows the first five feature sequences, the total being 799. The important thing to pay attention to here is the length of each sequence, as they should all be the same length for alignment and, later, taxonomic assignment. Aligning sequences of the same length is not only easier, but is more effective in identifying sequence similarities for constructing phylogenetic trees. If I scroll down this table, I can see that all 799 sequences are 137 basepairs long, which means that they are ready to be aligned.

command used: *feature-table tabulate seqs* from Obtaining, Denoising, and Merging Data

</details>

<details>

<summary>

### Taxa Visualization

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/559a0bfb-61b7-47ba-ba93-f95ee16d128b)

This is the first five rows of a table containing the taxa and confidence of each feature. These taxonomic assignments resulted from aligning the sequences and incorporating a 16s rRNA classifier. This table is helpful for comparing the corresponding taxa of each feature, and this data will be used to create a phylogenetic tree.

command used: *metadata tabulate* from Classifying Sequences

</details>

<details>

<summary>

### Phylogenetic Tree Visualization

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/407e5cf6-182c-439d-996a-376e0ee7274d)

This phylogenetic tree shows the relationships between taxa and was generated using a silva 16s rRNA classifier. The branches in the center of this circular plot are color coded by taxonomic class, and the outer layer is colored by treatment group. The control is in red, the treatment is in orange, and the donor is in blue. A phylogeny like this gives insight into the commonalities of different taxa and how they have evolved.

command used: *empress community-plot* from Making Phylogenetic Tree

</details>

<details>

<summary>

### Alpha Rarefaction and Diversity Visualizations

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/90cf1758-3448-4001-8474-8816eb104f78)

This is an alpha rarefaction plot that shows how sequence depth affects Faith's phylogenetic diversity, which is one of the diversity metrics that was used for this analysis. The control is in dark blue and the treatment is in light blue. A sequence depth of 876 was chosen after filtering the samples and viewing the minimum frequency. This graph is used to make sure that this depth is high enough to hold most of the diversity in the samples. This means that the diversity metric should stabilize lower than the chosen depth of coverage. In this case, Faith's pd stabilizes around 500, indicating that the majority of diversity was contained and there is still room to further analyze the diversity metrics.

command used: *diversity alpha-rarefaction* from Assessing Diversity Metrics

<br/>

<br/>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/f86a4179-2de3-4dc1-8509-118f4c061a19)

This boxplot shows the treatment group vs observed features, which is the alpha diversity metric. This plot shows species richness and diversity.

command used: *diversity alpha-group-significance* from Assessing Diversity Metrics

<br/>

<br/>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/ee3f1b37-bdff-4e14-a3d4-1b401ac17f7d)

This regression scatter plot shows how the number of weeks and treatment group affect the observed features metric. Looking at the graph, there is a slight positive correlation between weekly treatment and observed features. This means that the treatment group will have more diversity as time progresses.

command used: *longitudinal linear-mixed-effects* from Assessing Diversity Metrics

</details>

<details>

<summary>

### Beta Diversity Visualization

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/f6047523-246c-4692-bb2e-da3b28e3cd20)

This umap plot shows the unweighted beta diversity unifrac matrices. Each color represents a subject and each shape represents a sample method. The spheres represent stools and the diamonds represent swabs. The subjects are grouped near their own sample types. This plot is useful for visualizing beta diversity unifrac data and examining differences between samples.

command used: *emeror plot* from Assessing Diversity Metrics

</details>

<details>

<summary>

### Volatility Control Visualization

</summary>

![image](https://github.com/tesskeating/gen_711_final_project/assets/157992900/eeb8d827-eb26-49ee-923f-60e7e2047d68)

This is a volatility control plot that shows features that are associated with changes over time. In this case, the metric is families of bacteria, and the orange line is control and the blue line is treatment. Looking at the graph, the groups of bacteria within each sample changed over the 18 week period and in different ways. For example, the organisms from the control group peaked at 8 weeks, and the treated organisms peaked at 18 weeks. Comparisons like these can be made at the taxonomic and genus levels as well if matched using the same method.

command used: *longitudinal feature-volatility* from Assessing Diversity Metrics

</details>

</details>

<details>

<summary>

## Conclusions and Sources

</summary>

The main issues that I ran into while working on this project had to do with getting the empress command and pushing from my local repo to my github repo. I spent a while trying to figure out how to install empress on my laptop so that I could use it on vscode when qiime was activated. It only worked when I used the empress conda environment that Kaleb made. I also forgot to initially connect my github repo to my local one in vscode, so I was unable to run *git remote add origin*. It took a lot of trial and error, but I ended up having to clone my github repo into a new directory in vscode, transfer the files from my original project directory to the new one, and then push to github.

<br/>

All sources that I used for this project are listed below.

Kang, DW., Adams, J.B., Gregory, A.C. et al. Microbiota Transfer Therapy alters gut ecosystem and improves gastrointestinal and autism symptoms: an open-label study. Microbiome 5, 10 (2017). https://doi.org/10.1186/s40168-016-0225-7

https://docs.qiime2.org/2024.2/tutorials/fmt/

https://docs.qiime2.org/2022.2/tutorials/phylogeny/#sequence-alignment

https://zenodo.org/records/6395539#.ZGE7pHbMJhE

https://docs.qiime2.org/2024.2/tutorials/feature-classifier/

https://docs.qiime2.org/2024.2/tutorials/phylogeny/#fasttree

https://library.qiime2.org/plugins/empress/32/

https://github.com/biocore/empress#tutorial-using-empress-in-qiime-2

https://docs.qiime2.org/2024.2/tutorials/filtering/

https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/040-even-sampling.html

https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/050-core-metrics.html

https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/060-alpha-diversity.html

https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/070-beta-diversity.html

https://docs.qiime2.org/jupyterbooks/cancer-microbiome-intervention-tutorial/030-tutorial-downstream/080-longitudinal.html
