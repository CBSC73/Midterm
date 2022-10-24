Midterm
================
CB
2022-10-23

# **Title: Influenza Vaccine Uptake by Region and Age Group from 2012-2019 in the United States**

### **Introduction: Pregnant women and their newborns are at higher risk for severe illness from Influenza virus infection(Ref). Influenza during pregnancy can lead to severe maternal respiratory illness requiring hospitalization. It can also be a serious condition for infants (babies under 1 year of age), especially during the neonatal period (first 30 days of life) and for those with pre-existing respiratory conditions such as bronchopulmonary dysplasia (Ref). The yearly influenza vaccine has a long track record of safety and efficacy during pregnancy and is recommended by the Centers for Disease Control (CDC) for all pregnant women (Ref). Despite this recommendation by the CDC and the American College of Obstetrics (ref), many women choose not to receive the vaccination during pregnancy (ref). The objective of this qualitative data analysis is two fold, first to examine factors associated with low vaccine uptake. Specifically, age group and location. Second, to examine these trends over time to see whether uptake is increasing or decreasing. Identifying those pregnant women less likely to get vaccinated can help inform where efforts to promote vaccine utilization are needed most.**

``` r
library(data.table)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:data.table':
    ## 
    ##     between, first, last

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(tidyverse)
```

    ## ── Attaching packages
    ## ───────────────────────────────────────
    ## tidyverse 1.3.2 ──

    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.8     ✔ stringr 1.4.1
    ## ✔ tidyr   1.2.0     ✔ forcats 0.5.2
    ## ✔ readr   2.1.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::between()   masks data.table::between()
    ## ✖ dplyr::filter()    masks stats::filter()
    ## ✖ dplyr::first()     masks data.table::first()
    ## ✖ dplyr::lag()       masks stats::lag()
    ## ✖ dplyr::last()      masks data.table::last()
    ## ✖ purrr::transpose() masks data.table::transpose()

``` r
library(leaflet)
library(dtplyr)
library(knitr)
library(ggplot2)
```

    ## Warning: One or more parsing issues, see `problems()` for details

![](Midterm1_files/figure-gfm/create%20first%20table-1.png)<!-- -->

#### Figure 1. This figure demonstrates the change in Influenza vaccination uptake among pregnant women in the U.S. over time by age group. The timeframe is between the years 2012 and 2019. WOmen 35 years old and above tend to have higher vaccination rates and those aged 18-24 years have the lowest. This suggests that as women get older they are more likely to get the influenza vaccine during pregnancy. It appears that comparing 2012 to 2019 that the gap vaccination rate differences between age groups is shrinking, with the years 2018 and 2019 having nearly equal rates.

``` r
vax%>%
  filter(Age ==">=18 Years", Year == 2012 | Year == 2019) %>% 
  ggplot(aes(y=Estimate, x = region, fill = region)) +   
  geom_boxplot(color="black")+
  labs(title="Influenza Vaccination Rate Among Pregnant Women in the U.S. 2012 vs 2019",  y= "Vaccination Rate (%)")+
    theme(axis.title.x=element_blank())+
scale_fill_brewer(palette = "Reds")+
  facet_wrap(~Year, nrow=1)
```

![](Midterm1_files/figure-gfm/compare%20vaccine%20rates%20by%20region%20over%20time-1.png)<!-- -->

#### Figure 2. This boxplot figure shows Influenza vaccination rate among pregnant women in the United States by region between the years 2012 and 2019. This figure shows that in 2012 and 2019 the South has had the lowest vaccination rates. However this vaccination rate gap has grown considerably over time. In 2012 the West had the highest vaccination rate but over time this has gone down relative to the other region and in 2019 it was the Northeast with the highest rate.
