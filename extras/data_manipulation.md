---
layout: page
title: Data Manipulation
summary: "Basic data manipulation in Galaxy, including filtering, sorting, and reformatting text-based datasets."
hide: "yes"
---

---
In this tutorial, we will use as our dataset a table with results from the Olympics, 
from the games in Athens in 1896 until Tokyo in 2020. 

The objective is to familiarize you with a large number of the most important data manipulation tools in Galaxy. 

 The dataset contains 234,522 rows and 17 columns. 
 Each row corresponds to an individual athlete competing in an individual Olympic event. The columns are:

* athlete_id - Unique number for each athlete
* name - Athlete’s name 
* sex - M or F 
* birth_year - 4-digit number 
* birth_day - e.g. 24 July 
* birth_place - town and/or country 
* height - In centimeters (or NA if data not known)
* weight - In kilograms (or NA if data not known)
* team - Team name 
* noc - National Olympic Committee 3-letter code 
* games - Year and season 
* year - Integer 
* season - Summer or Winter 
* city - Host city 
* sport - Sport 
* event - Event 
* medal - Gold, Silver, Bronze (or NA if no medal was won)

---

Here is an overview table of the different data manipulations in this tutorial

| Operation            | Description                                                       | Galaxy Tool |
|----------------------|-------------------------------------------------------------------|-------|
| Convert format       | Change the file format                                           | Edit attributes |
| Word count           | Count the number of lines, words and characters in a file        | Line/Word/Character count |
| Sort on a column     | Change the order of the rows based on values in one or more columns | Sort  |
| Filter               | Remove rows based on values in one or more columns               | Filter |
| Counting             | Count occurrences of values in a column                          | Count, Datamash |
| Group on a column    | Perform simple operations (count, mean, min, max, etc.)          | Group, Datamash |
| Compute on rows      | Derive new column values from existing ones                      | Compute |
| Find and Replace     | In a specific column                                             | Column Regex Find and Replace |
| Find and Replace     | On every line                                                    | Regex Find and Replace |
| Join two Datasets    | Join side by side on a specified field                           | Join two Datasets |
| Concatenate datasets | Concatenate one after the other                                  | Concatenate datasets |
| Remove Beginning     | Good for removing header lines                                   | Remove beginning of a file |
| Select First lines   | Good for finding top 10s or saving header lines                  | Select first lines |
| Cut Columns          | By header name                                                   | Remove columns by heading |
| Cut Columns          | By column number                                                 | Cut columns from a table, Advanced Cut columns from a table |
| Paste                | Two files side by side                                           | Paste |
| Split file           | Based on values of a column                                      | Split |
| Unique               | Remove duplicate rows                                            | Unique|


---

## Quick Start

1. Create a new History
2. Rename your history to be meaningful and easy to find.
3. Upload the  dataset `olympics.tsv`
    ```shell 
    https://zenodo.org/record/6803028/files/olympics.tsv 
    ```
4. View <span class="fa fa-fw fa-eye"></span> the dataset
    ![]({{site.url}}/images/olympic-dataset.png)
5. Rename <span class="fa fa-fw fa-pencil"></span> the dataset to `olympics`

<span class="fa fa-fw fa-question-circle"></span> **Question**
* What is the format of the file? 
* What does each row represent? 
* How many lines are in the file? (`Line/Word/Character count` Tool)
* How many columns?

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## File Format Conversion

1. Convert Tabular to CSV
2. View <span class="fa fa-fw fa-eye"></span> the dataset 
3. Rename <span class="fa fa-fw fa-pencil"></span> the dataset to `olympics.csv`. 

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Sorting

We will sort the file in chronological order based on the year of the Olympic games (column ??)

1. Open the `Sort - data in ascending or descending order` Tool
   * *Number of header lines*: 1
   * *Sort Dataset*: olympics.tsv 
   * *on column*: Column 12 
   * *in*: Ascending order 
   * *Flavor*: Numeric sort
2. **Run Tool**
3. Rename <span class="fa fa-fw fa-pencil"></span> the resulting file to `Olympics in chronological order`
4. View <span class="fa fa-fw fa-eye"></span> the sorted dataset
5. <span class="fa fa-fw fa-question-circle"></span> **Question**
    - Which athlete is listed at the top now? 
    - Which discipline (sport) did they compete in?
<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

### Sort on multiple columns at once
Now, we want to sort twice, first by year, an then within each year, we sort again alphabetically by name.

1. **Re-run** <span class="fa fa-fw fa-refresh"></span> the `Sort - data in ascending or descending order` Tool
2. All parameter from the first step should already be set for you, and should remain the same
3. Insert Column selections:
   * *on column*: Column 2 
   * *in*: Ascending order 
   * *Flavor*: Alphabetical sort
4. **Run Tool**
5. <span class="fa fa-fw fa-question-circle"></span> **Question**
    - Which athlete is listed at the top now? 
    - Which discipline (sport) did they compete in?
6. View <span class="fa fa-fw fa-eye"></span> the sorted dataset

<span class="fa fa-fw fa-gears"></span> **Exercises**
-  Reverse the sort: 
    1. Which athlete comes last by alphabet, in the most recent Olympics?
  -  Sort by height:
  1. What is the height of the tallest competing athlete? Which athlete(s) are of this height? 
2. What is the shortest? 
3. Who was the tallest athlete from the most recent Olympics? How tall were they?

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Filtering
We will filter the file to show only winter Olympics

1. Look at the `olympics.tsv` file. Which column contains this information?
2. Open the tool `Filter data on any column using simple expressions`
   - *Filter*: olympics.tsv
   - *With the following condition*: c13=='Winter'
   - *Number of header lines to skip*: 1
3. **Run Tool**
4. View <span class="fa fa-fw fa-eye"></span> the filtered dataset
5. <span class="fa fa-fw fa-question-circle"></span> **Question**
   - How many lines are in this file?
6.  **Re-run** <span class="fa fa-fw fa-refresh"></span> the step for the Summer Olympics 
7. Rename <span class="fa fa-fw fa-pencil"></span> both 

<span class="fa fa-fw fa-gears"></span> **Exercises**

1. How many gold medals were handed out? 
2. How many total medals? 
3. How many medals were handed out during the 2018 Olympics? 
4. How many medals were won by individuals with a height between 170 and 180 cm? 
5. How many gold medals were won by individuals shorter than 160cm or taller than 190?

<span class="fa fa-fw fa-lightbulb-o"></span> **Solutions**

1. **8,110** (Expression: `c17=='Gold'`)
2. **24,633** (Expression: `c17=='Gold' or c17=='Silver' or c17=='Bronze'`, or `c17!='NA'`)
3. **131** (Expression: `c17=='Gold' and c12==2018` (note: do not use quotes around 2018, as it is a numerical value))
4. **8,086** (Expression: `c17!='NA' and c7>=170 and c7<=180`)
5. **812** (Expression: `c17=='Gold' and (c7<160 or c7>190)` (note: parentheses are important here))

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Counting
### Count occurrences of values in columns
Let’s start by simply counting how many different Olympic Games we have in our dataset, 
and how many times it appears (so how many participations there were each year)

1. `Count occurrences of each record` with the following parameters:
   * *from dataset*: olympics.tsv 
   * *Count occurrences of values in column(s)*: Column 11
   * *How should the results be sorted?*: most common values first
2. View <span class="fa fa-fw fa-eye"></span> the result


<span class="fa fa-fw fa-question-circle"></span> **Question**
1. How many different Olympic games are in our file?
2. Which Olympic games had the most participations?

Let’s try counting the number of men and women in each olympic games.
1. `Count occurrences of each record` with the following parameters:
   * *from dataset*: olympics.tsv
   * *Count occurrences of values in column(s)*: Column 11, Column 3
   * *How should the results be sorted?*: most common values first
2. View <span class="fa fa-fw fa-eye"></span> the result

<span class="fa fa-fw fa-question-circle"></span> **Question**
1. How many women were in the first Olympic games? 
2. Which Olympic games had the most women participants? 

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

### Counting number of different sports per Olympic Games
We will now determine how many different sport there were in each of the different Olympics
1. `Datamash` with the following parameters: 
   * <span class="fa fa-fw fa-file"></span> *Input tabular dataset*: `olympic.tsv`
   * *Group by fields*: 11 (game column)
   * *Input file has a header line*: Yes
   * *Print header line*: Yes
   * *Sort input*: Yes
   * *Ignore case when grouping*: Yes
   * In *Operation to perform on each group*:
       * *Type*: Count Unique values
       * *On column*: c15 (sport column)
2. View <span class="fa fa-fw fa-eye"></span> the result
3. *Rename* the output to something descriptive

<span class="fa fa-fw fa-question-circle"></span> **Question**
1. How many sport were in the first Olympics? How many in the latest?
2. Which Olympics had the most different sports?

<span class="fa fa-fw fa-gears"></span> **Exercises**

1. Which country has had the most participations in the Olympics? 
2. How many countries participated in the first Olympics? How many in the last?

<span class="fa fa-fw fa-lightbulb-o"></span> **Solutions**

1 - `Count` Tool with the following parameters: 
   - *from dataset*: olympics.tsv 
   - *Count occurrences of values in column(s)*: Column 9 (the team column)
   - *How should the results be sorted?*: With the most common values first

This gives an output like:

```text
17286	United States
11700	France
10230	Great Britain
8898	Italy
7988	Canada
```

2 - `Datamash` Tool with the following parameters: 
   - *Input tabular dataset*: olympics.tsv
   - *Group by fields*: 11 (the games column)
   - *Input file has a header line*: yes 
   - *Sort Input*: yes 
   - *Operation to perform on each group*:
     - *Type*: Count Unique values 
     - *On Column*: Column: 9 (the team column)

     This gives an output like:
```text
  1896 Summer Olympics	15
  1900 Summer Olympics	29
  1904 Summer Olympics	13
  ...
  2016 Summer Olympics	280
  2018 Winter Olympics	108
  2020 Summer Olympics	250
```
<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Grouping
Often we may want to group rows based on a value in a column, and perform some operation on the resulting rows. 
For example we would like to group the olympics data by one value (e.g. year, country, sport), 
and determine some value for each group (e.g. number of medals won, average age of athletes, etc).

We can use the `Datamash` tool for this purpose.

### Tallest athlete per sport
1. `Datamash` with the following parameters: 
   * <span class="fa fa-fw fa-file"></span> *Input tabular dataset*: `olympic.tsv`
   * *Group by fields*: 15
   * *Input file has a header line*: Yes
   * *Print header line*: Yes
   * *Sort input*: Yes
   * *Ignore case when grouping*: Yes
   * Skip NA or NaN values”: Yes
   * In *Operation to perform on each group*:
       * *Type*: Maximun
       * *On column*: c7
2. View <span class="fa fa-fw fa-eye"></span> the result

<span class="fa fa-fw fa-question-circle"></span> **Question**
1. How tall was the tallest athlete in basketball? 
2. And what about karate?

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---
### Grouping on multiple columns
The question we would like to answer here, is what is the average height for men and women per sport?

1. `Datamash` with the following parameters:
   * <span class="fa fa-fw fa-file"></span> *Input tabular dataset*: `olympic.tsv`
   * *Group by fields*: 15,3 (sport and sex column)
   * *Input file has a header line*: Yes
   * *Print header line*: Yes
   * *Sort input*: Yes
   * *Ignore case when grouping*: Yes
   * Skip NA or NaN values”: Yes
   * In *Operation to perform on each group*:
      * *Type*: Mean
      * *On column*: c7
2. View <span class="fa fa-fw fa-eye"></span> the result


<span class="fa fa-fw fa-gears"></span> **Exercises**
1. How tall is the shortest woman Badminton player to win a gold medal? 
2. What is the average height and standard deviation of athletes from Denmark (DEN) in the 1964 Olympics?

<span class="fa fa-fw fa-lightbulb-o"></span> **Solutions**
1. `Datamash` Tool with the following parameters:  
    - *Input tabular dataset*: olympics.tsv 
    - *Group by fields*: 17,15,3 (The medal, sports, and the sex columns)
    - *Sort input*: yes 
    - *Input file has a header line*: yes 
    - *Print header line* yes 
    - *Skip NA or NaN values*: yes 
    - *Operation to perform on each group*:
        - *Type*: Minimum 
        - *On Column*: Column: 7
    
      This will give an output like below, scroll down to find the gold medalists, then badminton, then F 
```text
   GroupBy(medal)	GroupBy(sport)	GroupBy(sex)	min(height)
Bronze	Alpine Skiing	F	156
Bronze	Alpine Skiing	M	167
Bronze	Archery	F	155
Bronze	Archery	M	166
Bronze	Art Competitions	F	-inf
Bronze	Art Competitions	M	172
Bronze	Artistic Gymnastics	F	136
...
```
   

2. `Datamash` Tool with the following parameters: 
   - *Input tabular dataset*: olympics.tsv 
   - *Group by fields*: 12,9 (year and team columns)
   - *Sort input*: yes 
   - *Input file has a header line*: yes 
   - *Print header line*: yes 
   - *Skip NA or NaN values*: yes 
   - *Operation to perform on each group*:
     - *Type*: Mean 
     - *On Column*: Column: 7 
   - *Operation to perform on each group*:
     - *Type*: Population Standard deviation 
     - *On Column*: Column: 7

    This will give an output like below:

```text
GroupBy(year)	GroupBy(team)	mean(height)	pstdev(height)
1896	Australia	nan	nan
1896	Austria	nan	nan
1896	Belgium	nan	nan
1896	Bulgaria	nan	nan
1896	Denmark	nan	nan
1896	France	167.62962962963	4.6836844324555
...

```
 
<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Computing
Sometimes we want to use the data in our column to compute a new value, and add that to the table. 
As an example, let’s calculate the age of each athlete at the time of participation, and add this as a new column to our dataset.

1. `Compute on rows` tool with the following parameters
   * <span class="fa fa-fw fa-file"></span> *Input file*: `olympic.tsv`
   * *Input has a header line with column names?*: Yes
   * In *Expressions*:
     * *Add expression*: int(c12)-int(c4) (year column minus the year_of_birth column)
     * *Mode of the operation?*: Append
     * *The new column name*: age
   * Under *Error handling*:
     * *Autodetect column types*: No
     * *If an expression cannot be computed for a row*: Fill in a replacement value
     * *Replacement value*: NA (not available)
2. View <span class="fa fa-fw fa-eye"></span> the result
3. *Rename* the output to something descriptive


<span class="fa fa-fw fa-question-circle"></span> **Question**
- How old was Arnaud Boetsch during his Olympic tennis participation?

<span class="fa fa-fw fa-gears"></span> **Exercises**
- Calculate BMI (weight/height<sup>2</sup>) for all athletes and add it as a new column directly after the existing height and weight columns.(Remember that our height is in cm, and the formula expects height in meters)

<span class="fa fa-fw fa-lightbulb-o"></span> **Solutions**
- `Compute on rows` Tool with the following parameters: 
  - *Input file*: olympics.tsv 
  - *Input has a header line with column names?*: Yes 
  - In *Expressions*:
    - *Add expression*: `int(c8)/(int(c7)*int(c7))*10000`
    - *Mode of the operation?*: Insert 
    - *Insert new column before existing column number*: 9 
    - *The new column name*: BMI 
  - Under *Error handling*:
  - *Autodetect column types*: No 
    - *If an expression cannot be computed for a row*: Fill in a replacement value 
    - *Replacement value*: NA (not available)
 

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Find and Replace
Our file uses a mix of Athina and Athens to indicate the Capital City of Greece in the city column. 
Let’s standardize this by replacing occurrences of Athina with Athens.

1. `Column Regex Find and Replace` tool with the following parameters: 
   * *Select cells from*: olympics.tsv
   * *using column*: Column 14
   * *Check*:
     * *Find Regex*: Athina
     * *Replacement*: Athens
2. View <span class="fa fa-fw fa-eye"></span> the result

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Removing Columns
We can remove columns from a table using either `Remove columns by heading` if your table has a header line, 
or `Cut columns from a table` if it does not (in this case we just indicate columns by their number). 
These tools can also be used to change the order of columns in your file. 
There is also the tool `Advanced Cut columns from a table` that offers a few more options.

Suppose we want to simplify our file a bit. All we want is file with 4 columns: athlete name, sport, olympic games, and medals.

1. `Remove columns by heading` tool with the following parameters: 
   * *Tabular File*: olympics.tsv 
   * *Header name*: name 
   * *Header name*: sport 
   * *Header name*: games 
   * *Header name*: medals 
   * *Keep named columns*: Yes
2. View <span class="fa fa-fw fa-eye"></span> the result

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Unique
Let’s say we would like to create a list of all unique athletes (id and name).

1. `Cut columns from a table` tool using the following parameters: 
   * *Cut Columns*: c1,c2 
   * *Delimited By*: TAB 
   * *From*: olympics.tsv
2. View <span class="fa fa-fw fa-eye"></span> the result
3. `Unique - occurrences of each record` tool with the following parameters: 
   * *File to scan for unique values*: output from the first step
4. View <span class="fa fa-fw fa-eye"></span> the result

<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---

## Concatenating
Our dataset was created in 2021, but since then we’ve had another Olympic event, 
the 2022 Winter Olympics in Beijing. 
If we have the same data for this latest Olympics, 
we could simply add the rows from the 2022 games to our current file with data, 
in order to create a single file with all data from 1896 to 2022.

1. Upload the  dataset `olympics.tsv`
    ```shell 
    https://zenodo.org/record/6803028/files/olympics_2022.tsv
    ```
2. `Remove beginning of a file`  with the following parameters: 
   * *Remove first*: 1
   * *from*: olympics_2022.tsv
3. `Concatenate datasets tail-to-head` with the following parameters: 
   * *Concatenate Datasets*: olympics.tsv 
   * *Insert Dataset*: output from previous step 1 (2022 data without the header)


<p style="text-align:right"><a href="{{site.url}}{{page.url}}"><strong>Go Up</strong><span class="fa fa-fw fa-arrow-up"></span></a></p>
---
