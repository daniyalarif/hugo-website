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

<script src="{{< blogdown/postref >}}index.en_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index.en_files/datatables-css/datatables-crosstalk.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.en_files/datatables-binding/datatables.js"></script>
<script src="{{< blogdown/postref >}}index.en_files/jquery/jquery-3.6.0.min.js"></script>
<link href="{{< blogdown/postref >}}index.en_files/dt-core/css/jquery.dataTables.min.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index.en_files/dt-core/css/jquery.dataTables.extra.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.en_files/dt-core/js/jquery.dataTables.min.js"></script>
<link href="{{< blogdown/postref >}}index.en_files/crosstalk/css/crosstalk.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.en_files/crosstalk/js/crosstalk.min.js"></script>

------------------------------------------------------------------------

#### Election Date: 13 Sept,2021

#### Analysis Date: 14 Sept,2021

------------------------------------------------------------------------

<br>
<br>

1.  Loading Libraries

``` r
library(readxl) # for reading excel file
library(tidyverse) # for data wrangling
library(ggplot2) # for plotting
library(ggparliament) # for parliament plot
library(dplyr) # for pipes
library(DT) # DT Tables
```

<br>
<br>

2.  Read excel file

``` r
# read_excel("...")
```

<br>
<br>

Arbeiderpartiet got the most seats: **48**

``` r
datatable(Valg)
```

<div id="htmlwidget-1" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","vertical":false,"data":[["1","2","3","4","5","6","7","8","9","10"],[2021,2021,2021,2021,2021,2021,2021,2021,2021,2021],["Norway","Norway","Norway","Norway","Norway","Norway","Norway","Norway","Norway","Norway"],["Storting","Storting","Storting","Storting","Storting","Storting","Storting","Storting","Storting","Storting"],["Arbeiderpartiet","Hoyre","Senterpartiet","Fremskrittspartiet","Sosialistisk Venstreparti","Rodt","Venstre","Kristeliq Folkeparti","Miljopartiet De Gronne","Pasientfokus"],["AP","H","Sp","Frp","SV","R","V","KrF","MdG","Other"],[48,36,28,21,13,8,8,3,3,1],[0,0,0,0,0,0,0,0,0,0],["#df1a21","#87acd7","#217121","#005194","#a51818","#e73446","#53be29","#ffaf10","#67962e","#2d3326"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>year<\/th>\n      <th>country<\/th>\n      <th>house<\/th>\n      <th>party_long<\/th>\n      <th>party_short<\/th>\n      <th>seats<\/th>\n      <th>government<\/th>\n      <th>colour<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,6,7]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>

3.  Take data and transform for ggparliament

``` r
No_Valg <- parliament_data(election_data = Valg,
                    type = "semicircle",
                    parl_rows = 4,
                    party_seats = Valg$seats)
```

<br>
<br>

4.  Plotting the data.

``` r
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

https://github.com/daniyalarif/Reporting\_Analytics/tree/main/StortingValg
