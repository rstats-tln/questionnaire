Pre course survey summary
================
Taavi Päll

Load required functions (libraries):

``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.8.0     ✔ stringr 1.3.0
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## ── Conflicts ───────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(googlesheets)
```

Download query spreadsheet:

``` r
(my_sheets <- gs_ls())
```

    ## # A tibble: 42 x 10
    ##    sheet_title  author perm  version updated             sheet_key ws_feed
    ##    <chr>        <chr>  <chr> <chr>   <dttm>              <chr>     <chr>  
    ##  1 Pre-course … "    … rw    new     2018-03-18 18:14:38 13ukx0z0… https:…
    ##  2 Tour de Rõu… "    … r     new     2018-03-18 10:27:05 1OR1g2lu… https:…
    ##  3 "          … sande… r     new     2018-03-12 07:10:16 14wc18fo… https:…
    ##  4 Registered … "   c… r     new     2018-02-08 15:56:28 1gDk6bQL… https:…
    ##  5 "  check_pu… "    … rw    new     2018-01-24 14:57:12 1QU_1Qwy… https:…
    ##  6 Moving Pict… "    … r     new     2018-01-11 22:29:41 149386JU… https:…
    ##  7 Sütemetsa 8… "  ti… r     new     2017-11-03 06:21:32 1RuNZBBB… https:…
    ##  8 Alasniidu N… "    … rw    new     2017-11-02 12:11:33 1kX-p8Bc… https:…
    ##  9 Haanja100 M… "    … r     new     2017-10-03 08:29:42 15TmC7IK… https:…
    ## 10 " testdatas… "    … rw    new     2017-09-13 10:24:46 1IOzPyBp… https:…
    ## # ... with 32 more rows, and 3 more variables: alternate <chr>,
    ## #   self <chr>, alt_key <chr>

Identify query sheet:

``` r
(surv <- gs_title("Pre-course survey (Responses)"))
```

    ## Sheet successfully identified: "Pre-course survey (Responses)"

    ##                   Spreadsheet title: Pre-course survey (Responses)
    ##                  Spreadsheet author: tapa741
    ##   Date of googlesheets registration: 2018-03-18 20:02:48 GMT
    ##     Date of last spreadsheet update: 2018-03-18 18:14:38 GMT
    ##                          visibility: private
    ##                         permissions: rw
    ##                             version: new
    ## 
    ## Contains 1 worksheets:
    ## (Title): (Nominal worksheet extent as rows x columns)
    ## Form Responses 1: 114 x 14
    ## 
    ## Key: 13ukx0z0KG6FxeMQYW71C56pwTRA4Hmx02EtdGAt9RAg
    ## Browser URL: https://docs.google.com/spreadsheets/d/13ukx0z0KG6FxeMQYW71C56pwTRA4Hmx02EtdGAt9RAg/

``` r
(responses <- surv %>% gs_read())
```

    ## Accessing worksheet titled 'Form Responses 1'.

    ## Parsed with column specification:
    ## cols(
    ##   Timestamp = col_character(),
    ##   `How big is your previous R experience?` = col_integer(),
    ##   `What operating system and version your computer is running?` = col_character(),
    ##   `Did you have running installation of the following software on your computer (check all that apply)?` = col_character(),
    ##   `Do you have GitHub account?` = col_character(),
    ##   `Do you have your own dataset (at least in mind) that you would like to use for individual project?` = col_character(),
    ##   `If you answered 'Yes' to previous question, please describe your dataset (name, how many rows/columns/number of variables, are your values categorical or continuous, csv, json, xls, html, etc.):` = col_character(),
    ##   `Email Address` = col_character()
    ## )

    ## # A tibble: 13 x 8
    ##    Timestamp  `How big is your … `What operating sy… `Did you have runnin…
    ##    <chr>                   <int> <chr>               <chr>                
    ##  1 3/8/2018 …                  5 macOS 10.13.3       R, Rstudio, Git      
    ##  2 3/14/2018…                  1 windows10           Git                  
    ##  3 3/14/2018…                  1 Win10               Git                  
    ##  4 3/14/2018…                  1 OS X 10.9.5         R, Rstudio, Git      
    ##  5 3/14/2018…                  5 Windows 10          R, Rstudio, Git      
    ##  6 3/14/2018…                  1 Win 10              Git                  
    ##  7 3/14/2018…                  1 Windows 10          Git                  
    ##  8 3/15/2018…                  1 win 10, 10.0.16299  Git                  
    ##  9 3/16/2018…                  1 macOS Sierra Versi… Git                  
    ## 10 3/17/2018…                  2 Windows 10 pro, ve… R, Rstudio, Git      
    ## 11 3/17/2018…                  1 windows 10          R, Rstudio, Git      
    ## 12 3/18/2018…                  1 Window 7            Git                  
    ## 13 3/18/2018…                  1 Windows 10 x64      R, Rstudio, Git      
    ## # ... with 4 more variables: `Do you have GitHub account?` <chr>, `Do you
    ## #   have your own dataset (at least in mind) that you would like to use
    ## #   for individual project?` <chr>, `If you answered 'Yes' to previous
    ## #   question, please describe your dataset (name, how many
    ## #   rows/columns/number of variables, are your values categorical or
    ## #   continuous, csv, json, xls, html, etc.):` <chr>, `Email Address` <lgl>

``` r
resp_gathered <- responses %>% 
  gather(key = key, value = value, -Timestamp)
```
