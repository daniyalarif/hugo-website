---
title: Norway Storting Valg
author: Daniyal
date: '2021-09-14'
slug: norway-storting-valg-preliminary-results
categories:
  - R
  - R Markdown
tags:
  - R Markdown
  - GGparliament
  - GGplot
subtitle: 'Preliminary Results'
summary: 'Preliminary Results'
authors: []
lastmod: '2021-09-14T12:00:34+02:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: [R Markdown]
---
<script src="{{< blogdown/postref >}}index.en_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index.en_files/lightable/lightable.css" rel="stylesheet" />

***

#### Election Date: 13 Sept,2021

#### Analysis Date: 14 Sept,2021

***
<br>
<br>


1) Loading Libraries


```r
library(readxl) # for reading excel file
library(tidyverse) # for data wrangling
library(ggplot2) # for plotting
library(ggparliament) # for parliament plot
library(dplyr) # for pipes
library(DT) # DT Tables
library(kableExtra) # Table Styling
```
<br>
<br>

2) Read excel file


```r
# read_excel("...")
```

  


<br>
<br>

3) Arbeiderpartiet got the most seats: **48**


```r
Valg %>%  kbl() %>%  kable_styling()
```

<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> year </th>
   <th style="text-align:left;"> country </th>
   <th style="text-align:left;"> house </th>
   <th style="text-align:left;"> party_long </th>
   <th style="text-align:left;"> party_short </th>
   <th style="text-align:right;"> seats </th>
   <th style="text-align:right;"> government </th>
   <th style="text-align:left;"> colour </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Arbeiderpartiet </td>
   <td style="text-align:left;"> AP </td>
   <td style="text-align:right;"> 48 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #df1a21 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Hoyre </td>
   <td style="text-align:left;"> H </td>
   <td style="text-align:right;"> 36 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #87acd7 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Senterpartiet </td>
   <td style="text-align:left;"> Sp </td>
   <td style="text-align:right;"> 28 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #217121 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Fremskrittspartiet </td>
   <td style="text-align:left;"> Frp </td>
   <td style="text-align:right;"> 21 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #005194 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Sosialistisk Venstreparti </td>
   <td style="text-align:left;"> SV </td>
   <td style="text-align:right;"> 13 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #a51818 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Rodt </td>
   <td style="text-align:left;"> R </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #e73446 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Venstre </td>
   <td style="text-align:left;"> V </td>
   <td style="text-align:right;"> 8 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #53be29 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Kristeliq Folkeparti </td>
   <td style="text-align:left;"> KrF </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #ffaf10 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Miljopartiet De Gronne </td>
   <td style="text-align:left;"> MdG </td>
   <td style="text-align:right;"> 3 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #67962e </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2021 </td>
   <td style="text-align:left;"> Norway </td>
   <td style="text-align:left;"> Storting </td>
   <td style="text-align:left;"> Pasientfokus </td>
   <td style="text-align:left;"> Other </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:left;"> #2d3326 </td>
  </tr>
</tbody>
</table>
<br>
<br>

4) Take data and transform for ggparliament


```r
No_Valg <- parliament_data(election_data = Valg,
                    type = "semicircle",
                    parl_rows = 4,
                    party_seats = Valg$seats)
```
<br>
<br>

5) Plotting the data.


```r
ggplot(No_Valg, aes(x, y, colour = party_long)) +
    geom_parliament_seats() + 
    geom_highlight_government(government == 1) +
    # add bar showing proportion of seats by party in legislature
    geom_parliament_bar(colour = colour, party = party_long) + 
    theme(legend.position = 'bottom'
          ) +
    labs(colour = NULL, 
         title = "Norway Storting Valg 2021",
         subtitle = "Preliminary results") +
    scale_colour_manual(values = No_Valg$colour,
                        limits = No_Valg$party_long)
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-6-1.png" width="6000" />
<br>
<br>

The files and links can be found on github Repo:

https://github.com/daniyalarif/Reporting_Analytics/tree/main/StortingValg
