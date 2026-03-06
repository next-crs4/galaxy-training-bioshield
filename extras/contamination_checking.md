---
layout: page
title: Checking expected species and contamination in bacterial isolate
summary: "Confirmation of the expected bacterial species and detection of possible contamination in isolate sequencing data."
hide: "yes"
---

---

When sequencing a genome, contamination from foreign organisms 
may be inadvertently mixed with the genomic material of the species of interest.  
For this reason, when working with bacterial isolates, 
it is crucial to verify that the expected species or strains are present in the data 
and to identify any potential contamination.

Confirming species identity and detecting contamination are essential 
to ensure the accuracy and reliability of the analysis, 
and to prevent misleading results that could affect downstream interpretations.

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Galaxy and data preparation

To illustrate the process of checking the expected species and potential contamination in a bacterial isolate,  
we will use the sequencing reads filtered with `fastp` 
in the [assembly tutorial]({{site.url}}/lectures/06.genome_assembky_of_a_bacterial_genome).

Before starting the analysis, prepare your Galaxy workspace as follows:

1. Create a new Galaxy history and give it a meaningful name.
2. Import the paired-end reads filtered with `fastp` by dragging and dropping them from the previous history (see [here]({{site.url}}/lectures/03.introduction_to_galaxy_analyses/#look-at-all-your-histories) for instructions on managing and copying datasets between histories).

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Taxonomic profiling

To find out which microorganisms are present,
we will compare the reads of the sample to a reference database,
i.e. sequences of known microorganisms stored in a database, using [Kraken2](https://ccb.jhu.edu/software/kraken2/)

### k-mer based taxonomic assignment

In the **k-mer approach for taxonomy classification**,
we use a database containing DNA sequences of genomes whose taxonomy we already know. On a computer,
the genome sequences are broken into **short pieces of length k** (called **k-mers**), usually **30bp**.

1. examines the **k-mers** within the query sequence,

2. searches for them in the **database**,

3. looks for where these are placed within the **taxonomy tree** inside the database,

4. makes the classification with the **most probable position**,

5. then maps k-mers to the **lowest common ancestor (LCA)** of all genomes known to contain the given k-mer.

<img src="{{site.url}}/images/kmers-kraken.jpg">

For this tutorial, we will use the [**PlusPF database**](https://benlangmead.github.io/aws-indexes/k2) which contains the Standard (archaea, bacteria, viral, plasmid, human, UniVec_Core), protozoa and fungi data.

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

###  Assign taxonomic labels with Kraken2

1. `Kraken2` Tool with the following parameters:
    - *Single or paired reads*: Paired Collection
        - *Collection of paired reads*: Input paired collection
      
    - *Confidence*: 0.1
   
    - *Minimum Base Quality*: 10
   
    - In *Create Report*:
        - *Print a report with aggregrate counts/clade to file*: Yes
   
    - *Select a Kraken2 database*: Prebuilt Refseq indexes: PlusPF

A **confidence score of 0.1** means that **at least 10%** of the k-mers should match entries in the database.
This value can be reduced if a less restrictive taxonomic assignation is desired.

<div style="border-left: 4px solid #d9534f; 
            padding: 12px; 
            background-color: #f8d7da; 
            margin: 20px 0;">
    <strong><span class="fa fa-fw fa-exclamation-triangle"></span> Warning:</strong>
    The execution of this tool can take approximately 4 hours. 
    To avoid unnecessary waiting time and server overload during the course, 
    please retrieve the precomputed outputs from the shared history.
    </div>

`Kraken2` will create two outputs for each dataset: **Classification** and **Report**

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

#### Classification

* **Classification**: tabular files with one line for each sequence classified by Kraken and 5 columns:
1. `C`/`U`: a one letter indicating if the sequence classified or unclassified
2. Sequence ID as in the input file
3. NCBI taxonomy ID assigned to the sequence, or 0 if unclassified
4. Length of sequence in bp (`read1|read2` for paired reads)
5. A space-delimited list indicating the lowest common ancestor (LCA) mapping of each k-mer in the sequence

For example, `562:13 561:4 A:31 0:1 562:3` would indicate that:
1. The first 13 k-mers mapped to taxonomy **ID #562**
2. The next 4 k-mers mapped to taxonomy **ID #561**
3. The next 31 k-mers contained an ambiguous nucleotide
4. The next k-mer was not in the database
5. The last 3 k-mers mapped to taxonomy **ID #562**

`|:| `indicates end of first read, start of second read for paired reads

![]({{site.url}}/images/kraken2_classification.png)

<span class="fa fa-fw fa-question-circle"></span> **Question**

1. Is the first sequence in the file classified or unclassified?
2. What is the taxonomy ID assigned to the first classified sequence?
3. What is the corresponding taxon

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

#### Report

* **Report**: tabular files with one line per taxon and 6 columns or fields:
  1. Percentage of fragments covered by the clade rooted at this taxon
  2. Number of fragments covered by the clade rooted at this taxon
  3. Number of fragments assigned directly to this taxon
  4. A rank code, indicating:
    - (**U**)nclassified
    - (**R**)oot
    - (**D**)omain
    - (**K**)ingdom
    - (**P**)hylum
    - (**C**)lass
    - (**O**)rder
    - (**F**)amily
    - (**G**)enus
    - (**S**)pecies
      
      Taxa that are not at any of these 10 ranks have a rank code that is formed by using
      the rank code of the closest ancestor rank with a number indicating the distance from that rank.

      E.g., **G2** is a rank code indicating a taxon is between genus and species and the grandparent taxon is at the genus rank.
  
  5. NCBI taxonomic ID number
  6. Indented scientific name

![]({{site.url}}/images/kraken2_report.png)

<span class="fa fa-fw fa-question-circle"></span> **Question**

1. How many taxa have been found? 
2. What are the percentage on unclassified? 
3. What are the domains found?

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Species extraction
In Kraken output, there are quite a lot of identified taxa with different levels. 
To extract the species level, we will use [Bracken](https://ccb.jhu.edu/software/bracken/)
(*Bayesian Reestimation of Abundance after Classification with Kraken*).

Instead of only using proportions of classified reads,
it takes a probabilistic approach to generate final abundance profiles.
It works by re-distributing reads in the taxonomic tree:
**Reads assigned to nodes above the species level are distributed down to the species nodes,
while reads assigned at the strain level are re-distributed upward to their parent species**

1. `Bracken` Tool with the following parameters:
   - *Kraken report file*: Report output of Kraken
   - *Select a kmer distribution*: PlusPF  (same as for Kraken)
   - *Level*: Species
   - *Produce Kraken-Style Bracken report*: yes

**NOTE!** It is important to choose the same database that you also chose for Kraken2

`Bracken` output file format (tabular):
* Taxon name
* Taxonomy ID
* Level ID (S=Species, G=Genus, O=Order, F=Family, P=Phylum, K=Kingdom)
* Kraken assigned reads
* Added reads with abundance re-estimation
* Total reads after abundance re-estimation
* Fraction of total reads

![]({{site.url}}/images/bracken_report.png)


<span class="fa fa-fw fa-question-circle"></span> **Question**
1. How many species have been found? 
2. Which the species has been the most identified? And in which proportion? 
3. What are the other species?

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Contamination identification

To explore `Kraken` report and specially to detect more reliably minority organisms or contamination, 
we will use [Recentrifuge](https://doi.org/10.1371/journal.pcbi.100696)


1. `Recentrifuge` with the following parameters:
   - *Select taxonomy file tabular formated*: classification of Kraken2 tool
   - *Type of input file (Centrifuge, CLARK, Generic, Kraken, LMAT)*: Kraken
   - In *Database type*:
   
     - *Cached database whith taxa ID*: latest
             
   - In *Output options*:
   
     - *Type of extra output to be generated (default on CSV)*: TSV
     - *Remove the log file*: Yes
             
   - In *Fine tuning of algorithm parameters*:
               
     - *Strain level instead of species as the resolution limit for the robust contamination removal algorithm; use with caution, this is an experimental feature*: Yes

`Recentrifuge` generates 3 outputs:

1. A statistic table with general statistics about assignations

    ![]({{site.url}}/images/recentrifuge_stats.png)

2. A data table with a report for each taxa

    ![]({{site.url}}/images/recentrifuge_data.png)

3. A HTML report with a Krona chart

   ![]({{site.url}}/images/recentrifuge_krona.png)


<span class="fa fa-fw fa-question-circle"></span> **Question**
1. What is the percentage of classified sequences? 
2. When clicking on Staphylococcus aureus, what can we say about the strains? 
3. Is there any contamination?

**NOTE!** There is no sign of a possible contamination. Most sequences are classified to taxon on 
the **Staphylococcus aureus** taxonomy. Only 4% of the sequences are not classified to Staphylococcus.

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Visualization of taxonomic assignment

Getting an overview of the assignation is not straightforward with the Kraken2 outputs directly.
Once we have assigned the corresponding taxa to each sequence, the next step is to properly visualize the data.
There are several tools for that:

* Krona
* [Pavian](https://fbreitwieser.shinyapps.io/pavian/)

### Visualisation using Krona

`Krona` creates an interactive HTML file allowing hierarchical data to be explored with zooming,
multi-layered pie charts.

With this tool, we can easily visualize the composition of the bacterial communities and
compare how the populations of microorganisms are modified according to the conditions of the environment.


#### Convert Kraken report file
`Kraken` outputs can not be given directly to `Krona`, they first need to be converted.

`Krakentools` is a suite of tools to work on Kraken outputs.
It include a tool designed to translate results of the Kraken metagenomic classifier
to the full representation of NCBI taxonomy.
The output of this tool can be directly visualized by the Krona tool.

1. `Krakentools: Convert kraken report file` Tool with the following parameters:
   - *Kraken report file*: Report collection of `Kraken`
2. Inspect the generated output

![]({{site.url}}/images/krakentools.png)

#### Generate Krona visualisation

Let’s now run `Krona`

1. `Krona pie chart` Tool with the following parameters:
   - *Type of input data*: Tabular
   - *Input file*: output of `Krakentools`
2. Inspect the generated file

![]({{site.url}}/images/krona_pie.png)

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

### Visualization using Pavian
[Pavian](https://fbreitwieser.shinyapps.io/pavian/) (pathogen visualization and more)
is an interactive visualization tool for metagenomic data.
It was developed for the clinical metagenomic problem to find a disease-causing pathogen in a patient sample,
but it is useful to analyze and visualize any kind of metagenomics data.

1. Download Report files from Report collection of `Kraken`
2. Upload Report files on Pavian server: [https://fbreitwieser.shinyapps.io/pavian/](https://fbreitwieser.shinyapps.io/pavian/)
3. Click on `Save table`
4. Click on `Result Overview`.
   This page shows the summary of the classifications in the selected sample set:


![]({{site.url}}/images/pavian.png)

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---