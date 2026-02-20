---
layout: page
title: From NCBI's Sequence Read Archive (SRA) to Galaxy
summary: "How can you download public sequencing data deposited in the NCBI Sequence Read Archive (SRA) into a Galaxy history for analysis?
"
hide: "yes"
---

---

The **[Sequence Read Archive (SRA)](https://www.ncbi.nlm.nih.gov/sra)** is the primary archive of unassembled reads operated by the 
**[US National Institutes of Health (NIH)](https://www.ncbi.nlm.nih.gov/)**. 

**SRA** is a great place to get the sequencing data that underlie publications and studies. 
The [study](https://www.science.org/doi/10.1126/science.abe3261) we are interested in for this tutorial is one on sequencing of SARS-CoV-2 viral isolates that were obtained 
in the Boston area in the first months of the COVID-19 pandemic.

So lets see how we can find its raw data in the **SRA**, 
and how we can get some of that data into Galaxy to analyze it. 

The **Acknowledgments section** of the publication mentions that raw reads from the study have been deposited 
in the **SRA** under **BioProject PRJNA622837** so that’s going to be our starting point.

   <img src="{{site.url}}/images/sra-aknow.png">

## Find the example data in the SRA

1. Go to NCBI’s SRA page by pointing your browser to [https://www.ncbi.nlm.nih.gov/sra](https://www.ncbi.nlm.nih.gov/sra)

2. In the search box enter `PRJNA622837[BioProject]`
   - **!!!** Oh, this finds a lot of samples (more than 22,200 at the time of writing)! This is because the BioProject ID we used is that of “SARS-CoV-2 Patient Sequencing from the Broad Institute”, which has seen many more sample submissions since the published study. Let’s refine our search a bit.
   
3. Replace your previous search with `PRJNA622837[BioProject] AND RNA-Seq[Strategy]`
   - This returns only those samples from the BioProject, for which the sequencing strategy was RNA-Seq. 
   - At the time of writing, 1908 hits are retained with this query, which is still more than the approximately 800 genomes mentioned in the publication, but we got a lot closer.
   
4. Instead of inspecting all 1908 hits one-by-one through the web interface, lets download the metadata for all samples in a single file
   - Click on the **Send to**: dropdown at the top of the search results list 
   - Under **Choose Destination**, select **Run Selector**
   - Click **Go**
   
   <img src="{{site.url}}/images/sra-get_runinfo.png">
   - You will be taken to the SRA Run Selector page, where you can browse all of the metadata of all search hits rather conveniently.
   
5. In the **Select table**, click **Metadata** in the **Download column**
   - This will download the metadata for all retrieved sequencing runs as a comma-separated text file.
   
   <img src="{{site.url}}/images/sra-metadata_from_run_selector.png">

**NOTE!!!** Note that the file we just downloaded is not sequencing data itself. Rather, it is metadata describing the data itself

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

##  Preparing data

**NOTE!** Please, use
* [https://usegalaxy.eu/](https://usegalaxy.eu/)
* [https://metagenomics.usegalaxy.eu/](https://metagenomics.usegalaxy.eu/)

### Upload metadata file 



1. Create a new history and Rename it
2. Upload the metadata file
3. Inspect its contents
   - You will see that this file contains the same metadata that you could preview on the SRA Run Selector page.
   
<img src="{{site.url}}/images/sra-metadata.png">
   
<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

### Filter metadata lines by collection date range

In Galaxy, it is rather easy to perform further filtering of the metadata records. 
For example, the publication mentions that the authors analyzed samples collected between **4 March and 9 May 2020**,



If you inspect the metadata, you should see a column Collection_Date. That looks useful!


1. `Filter data on any column using simple expressions` tool with following parameters:
   - *Filter*: the uploaded metadata 
   - *With following condition*: "2020-03-04" <= c11 <= "2020-05-09"
     - Column 11 (c11) is the Collection_Date column in this case. If your input has this column in a different position, you would need to adjust the filter condition above accordingly. 
   - *Number of header lines to skip*: 1

So now we are down to sequencing runs from the same date range as studied in the publication: 
though we still have more runs than samples discussed in the publication. 

Note, however, that the publication talks about assembled genomes, 
and it is possible that some of the sequencing runs listed in our metadata do not contain 
good enough data to assemble any SARS-CoV-2 genome information, 
or it could be that some viral samples got sequenced in several sequencing runs to obtain enough data.

We suggest to continue with just the following two interesting datasets:
SRR11954102 and SRR12733957. So let’s pull their identifiers out of the metadata file.

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

###  Extracting a subset of identifiers

1. `Select lines that match an expression` Tool with following datasets:
   - *Select lines from*: the metadata filter by collection date; output of `Filter` tool 
   - *that*: Matching 
   - *the pattern*: SRR12733957\|SRR11954102
2. `Advanced Cut` Tool with following datasets:
   -  *File to cut*: the metadata with only two runs retained; output of `Select` tool 
   - Under *Cut by*:
     - Column: 1 

At this point, you should have a dataset with just two lines and a single column with this content:

```text
SRR12733957
SRR11954102
```

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Retrieve selected sequencing data from the SRA

Now that we have our identifiers of interest extracted, 
we are ready to download the actual sequencing data. 
Since this is a very common need Galaxy offers a dedicated tool for the purpose of downloading sequencing data from the SRA identified via its run accession.

1. `Faster Download and Extract Reads in FASTQ` Tool with the following parameters: 
   - *select input type*: List of SRA accession, one per line
     - *sra accession list*: the dataset with the two run accessions; output of `Cut`

Several entries should have been created in your history panel when you submitted the previous job:

* **Pair-end data (fasterq-dump)**: Contains Paired-end datasets (*if available*)
* **Single-end data (fasterq-dump)**: Contains Single-end datasets (*if available*)
* **Other data (fasterq-dump)**: Contains Unpaired datasets (*if available*)
* **fasterq-dump log**: Contains Information about the tool execution

When the tool run is finished, you should find that only the Pair-end data collection contains any sequencing data, which makes sense as both samples have been paired-end sequenced on the Illumina platform. 

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Hands-On

Now, it's your turn! Retrieve the BioProject ID from this [article](https://www.researchsquare.com/article/rs-1560496/v1) and  upload the datasets to a new history in Galaxy.

In order to save time, we have pre-selected the samples that appeared to be the most significant. 

```text
SRR18739533 
SRR18739534
SRR18739542
SRR18739550
SRR18739557
SRR18739561
SRR18739563
SRR18739566
SRR18739571
```

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---
