---
layout: page
title: Introduction to Visualisations in Galaxy
summary: "Visualizations are vital for the interpretation of large datasets. 
Galaxy has numerous visualization options available.
"
hide: "yes"
---

---

## What is Data Visualisation?

* Making graphics to clearly convey data 
* Many different options

<img src="{{site.url}}/images/chart_types.png">

---

* More than just scatter plots and bar charts 
* Many domain-specific 
  * Protein folding, network graphs, trees, genome browsers

<img src="{{site.url}}/images/charts_examples2.png">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Why visualizations?

* A picture is worth 1000 words

* Anscombe’s Quartet. All these datasets share the same basic statistics:  same mean, standard deviation and correlation, yet when visualizing them it is revealed they have vastly different structures.

```r
X mean: 54.26, X SD: 16.76
Y mean: 47.83, Y SD: 26.93
Correlation: -0.06
```

<img src="{{site.url}}/images/anscombe-quartet-animated.gif">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

# Data Visualisation in Galaxy

---

## Genome Browsers

* Visualize the genome
  - mapped sequence reads, variants, genes, ..

<img src="{{site.url}}/images/sequencing.png">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Genome Browsers in Galaxy

* As display applications 
  * e.g. UCSC browser, IBV, IGB, .. 
  * accessed via links on dataset

<img src="{{site.url}}/images/display_options_bam.png">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## JBrowse

* `JBrowse` is not a display application like the previous examples
* Genome browser as a regular tool 
* Configure your settings

<img src="{{site.url}}/images/jbrowse_tool.png">

* Then interactively explore your genome

<img src="{{site.url}}/images/sequencing.png">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Galaxy Charts

* Accessed through Charts icon <span class="fa fa-fw fa-bar-chart"></span> on dataset 
* Different options depending on datatype


<img src="{{site.url}}/images/charts_list.png">

* After selecting chart type, can customize settings 
* Example: **Protein Viewer**


<img src="{{site.url}}/images/charts_pdbviewer.png">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Visualisation Tools

* Many tools for visualisation 
* Example: **Circos for circular data plots**


<img src="{{site.url}}/images/circos-sample-panel.png">


<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---
