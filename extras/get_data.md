---
layout: page
title: Getting data into Galaxy 
summary: "Importing local and public datasets into Galaxy."
hide: yes
---

---

## Many ways to get data into your workspace

1. Import using Get Data sources e.g. UCSC, [SRA]({{site.url}}/extras/from_sra_to_galaxy) 
2. Import from a Galaxy Data Library 
3. Import using Upload File
   * Import from your computer 
   * Directly enter text 
   * Import from a URL 
   * Import using FTP 
   * Import directly into Collection 
   * Import using Rule Builder

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

### Best method depends on where the data is, and how big it is

<img src="{{site.url}}/images/get_data_upload_logic.png">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## The Get Data toolbox section

* Click on the **Get Data** toolbox in the toolbox (the left panel)
* Expands to show data sources
  - The specific data sources available on your Galaxy instance are determine by the server's administrator
* All of these data sources can bring *datasets (files)* into your Galaxy *workspace (history)*

<table style="border:1px solid white;">
<tr>
<td style="background-color:white; border:1px solid white; vertical-align: top;">
<img src="{{site.url}}/images/get_data_boxed.png">
</td>
<td style="background-color:white; border:1px solid white; vertical-align: top;">
<img src="{{site.url}}/images/get_data_expanded.png">
</td>
</tr>
</table>


* Two large data sources you can access through Galaxy are UCSC and SRA
<table style="border:1px solid white;">
<tr>
<td style="background-color:white; border:1px solid white; vertical-align: top;">
<img src="{{site.url}}/images/get_data_ucsc.png">
</td>
<td style="background-color:white; border:1px solid white; vertical-align: top;">
<img src="{{site.url}}/images/get_data_sra.png">
</td>
</tr>
</table>


<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Import from Shared Data Library

* Top menu bar -> Shared Data -> **Data Libraries**
* Configured by a **Galaxy Administator**
* Can be imported directly into your history

<img src="{{site.url}}/images/get_data_data_libraries.png" width="30%">

<img src="{{site.url}}/images/get_data_import_library.png" width="100%">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Upload from your computer

* At the top of the Tools panel (on the left), click <span class="fa fa-fw fa-upload"></span> **Upload**
  ![]({{site.url}}/images/upload-data.png)
  This brings up a box:
  ![]({{site.url}}/images/upload_file_form_empty.png)

- The Upload File data source can import data:
    * from your computer 
    * by directly entering text 
    * using a URL 
    * and via FTP

### Choose files

<img src="{{site.url}}/images/upload_file_form_empty_local_choices.png" width="100%">

* Drag and drop is supported 
* as is the standard file selection using your browser.

### Set Metadata

* **Datatype** (e.g. FastQ, VCF, BAM, tabular, ..)
  * Galaxy will autodetect by default (sometimes guesses wrong)
* **Genome Build** (e.g. hg19, mm9, ..)
  * must be set manually (can be done later as well)

* Click Start, and then Close, and the new items show up in your history with the URL as their name.

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Import using URL

The data might already be available on a web server somewhere. 
To avoid downloading data to your computer and uploading to Galaxy in two steps, 
you can instruct Galaxy to directly fetch the data from a given URL.

* Select **Paste/Fetch data**

<img src="{{site.url}}/images/upload_file_form_empty_paste.png" width="100%">

* Enter the URLs (one per line) into the input box:

<img src="{{site.url}}/images/fetch_from_url.png" width="100%">

* Click **Start**, and then **Close**, and the new items show up in your history with the URL as their name.

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Import using FTP

* Why use FTP?
  * Older Galaxies did not support uploading files larger than 2GB in size 
  * Many people are very comfortable using FTP to upload large datasets and you can sometimes resume interrupted uploads.

* How to use FTP
  * The Galaxy server's administrator must have enabled FTP on the server 
  * You will need to create an account on that Galaxy Server 
  * You will need to install FTP software, or to run FTP from the shell

### Make sure you have an FTP client installed

* [FileZilla](https://filezilla-project.org/) is a free FTP client that is available on [Windows](https://filezilla-project.org/download.php?platform=win64), [MacOS](https://filezilla-project.org/download.php?platform=osx), and [Linux](https://filezilla-project.org/download.php?platform=linux) 
* There are many other options 
* If you don't already have an FTP client, download and install FileZilla.


<img src="{{site.url}}/images/FileZilla_logo.png" width="10%">

### Establish FTP connection to your Galaxy server

* Provide 
  * the instance's FTP server name (e.g. izs3.crs4.it, usegalaxy.org, ftp.usegalaxy.eu)
  * your full **username** (usually an email address) and **password**


<img src="{{site.url}}/images/filezilla.png" width="100%">

* Right click on the files and upload them.


<img src="{{site.url}}/images/filezilla_upload.png" width="100%">

### Where did my files go?

* File Upload menu -> **Choose FTP files**

<img src="{{site.url}}/images/upload_ftp_import.png" width="100%">

* Select files to import into your history 
* Click **Start**

<img src="{{site.url}}/images/choose_ftp_files.png" width="100%">

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Import directly into Collection

* Select **Collection** tab at top of upload menu 
* Add files as before (**upload from computer**, **paste/fetch**, **FTP**)

<img src="{{site.url}}/images/get_data_direct_collection1.png" width="100%">

* Choose collection type (at bottom)
* Set metadata (file type, genome build)
* Click **Build**


<img src="{{site.url}}/images/get_data_direct_collection2.png" width="100%">

* Name your collection 
* Click **Create** button


<img src="{{site.url}}/images/get_data_direct_collection3.png" width="100%">
<img src="{{site.url}}/images/get_data_direct_collection1.png" width="100%">


<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---
