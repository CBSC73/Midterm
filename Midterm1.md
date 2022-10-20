Midterm
================
CB
2022-10-19

# **Title: Influenza Vaccine Uptake by Region and Age Group from 2012-2019 in the United States**

## **Introduction: Pregnant women and newborns are at higher risk for severe illness from Influenza virus infection(Ref). Influenza during pregnancy can lead to severe maternal respiratory illness requiring hospitalization. It can also be a serious condition for infants (babies under 1 year of age), especially during the neonatal period (first 30 days of life) and for those with pre-existing respiratory conditions such as bronchopulmonary dysplasia (Ref). The yearly influenza vaccine has a long track record of safety and efficacy during pregnancy and is recommended by the Centers for Disease Control (CDC) for all pregnant women (Ref). Despite this recommendation, only approximately 50% of women receive the influenza vaccine during pregnancy (ref). The objective of this qualitative data analysis is two fold, first to examine factors associated with low vaccine uptake. Specifically, age group and location. Second, to examine these trends over time to see whether uptake is increasing or decreasing. Identifying those pregnant women less likely to get vaccinated can help inform where efforts to promote vaccine utilization are needed most.**

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

``` r
library(readr)
Vaccination_Coverage_among_Pregnant_Women_3_ <- read_csv("C:/Users/clair/Desktop/PM566/Vaccination_Coverage_among_Pregnant_Women (3).csv", 
    col_types = cols(`Survey Year_Influenza Season` = col_integer(), 
        Estimate = col_number(), `95CI` = col_skip(), 
        `Sample Size` = col_number()))
```

    ## Warning: One or more parsing issues, see `problems()` for details

``` r
View(Vaccination_Coverage_among_Pregnant_Women_3_)
```

``` r
vaxdata<-Vaccination_Coverage_among_Pregnant_Women_3_
dim(vaxdata)
```

    ## [1] 3621    8

``` r
head(vaxdata)
```

    ## # A tibble: 6 × 8
    ##   Vaccine   `Geography Type` Geography Survey …¹ Dimen…² Dimen…³ Estim…⁴ Sampl…⁵
    ##   <chr>     <chr>            <chr>         <int> <chr>   <chr>     <dbl>   <dbl>
    ## 1 Influenza States           Alaska         2012 Age     >=18 Y…    49.2     852
    ## 2 Influenza States           Arkansas       2012 Age     >=18 Y…    46.6     756
    ## 3 Influenza States           Colorado       2012 Age     >=18 Y…    56.1    1170
    ## 4 Influenza States           Delaware       2012 Age     >=18 Y…    41.6     981
    ## 5 Influenza States           Georgia        2012 Age     >=18 Y…    33.6    1007
    ## 6 Influenza States           Hawaii         2012 Age     >=18 Y…    42      1385
    ## # … with abbreviated variable names ¹​`Survey Year_Influenza Season`,
    ## #   ²​`Dimension Type`, ³​Dimension, ⁴​Estimate, ⁵​`Sample Size`

``` r
unique(vaxdata$Vaccine)
```

    ## [1] "Influenza" "Tdap"

``` r
unique(vaxdata$'Geography Type')
```

    ## [1] "States"   "National"

``` r
unique(vaxdata$Geography)
```

    ##  [1] "Alaska"               "Arkansas"             "Colorado"            
    ##  [4] "Delaware"             "Georgia"              "Hawaii"              
    ##  [7] "Illinois"             "Maine"                "Maryland"            
    ## [10] "Massachusetts"        "Michigan"             "Minnesota"           
    ## [13] "Missouri"             "Nebraska"             "New Jersey"          
    ## [16] "New Mexico"           "NY-City of New York"  "Ohio"                
    ## [19] "Oklahoma"             "Oregon"               "Pennsylvania"        
    ## [22] "United States"        "Rhode Island"         "Tennessee"           
    ## [25] "Utah"                 "Vermont"              "Washington"          
    ## [28] "West Virginia"        "Wisconsin"            "Wyoming"             
    ## [31] "New York"             "Iowa"                 "New Hampshire"       
    ## [34] "NY-Rest of state"     "Alabama"              "Connecticut"         
    ## [37] "Louisiana"            "Texas"                "Virginia"            
    ## [40] "Kansas"               "Kentucky"             "Montana"             
    ## [43] "North Carolina"       "North Dakota"         "Puerto Rico"         
    ## [46] "South Dakota"         "District of Columbia" "Indiana"             
    ## [49] "Mississippi"          "Florida"

``` r
unique(vaxdata$'Survey Year_Influenza Season')
```

    ## [1] 2012 2013 2014 2015 2016 2017 2018 2019

``` r
unique(vaxdata$'Dimension Type')
```

    ## [1] "Age"            "Race/Ethnicity"

``` r
unique(vaxdata$Dimension)
```

    ## [1] ">=18 Years"                           
    ## [2] "18-24 Years"                          
    ## [3] "25-34 Years"                          
    ## [4] ">=35 Years"                           
    ## [5] "Black, Non-Hispanic"                  
    ## [6] "Hispanic"                             
    ## [7] "Other or Multiple Races, Non-Hispanic"
    ## [8] "White, Non-Hispanic"

``` r
vaxdata1<-subset(vaxdata, `Dimension Type`=="Age")
table(vaxdata1$'Dimension Type')
```

    ## 
    ##  Age 
    ## 1824

``` r
dim(vaxdata1)
```

    ## [1] 1824    8

``` r
colSums(is.na(vaxdata1))
```

    ##                      Vaccine               Geography Type 
    ##                            0                            0 
    ##                    Geography Survey Year_Influenza Season 
    ##                            0                            0 
    ##               Dimension Type                    Dimension 
    ##                            0                            0 
    ##                     Estimate                  Sample Size 
    ##                           15                            0

``` r
vaxdata1 %>% drop_na(Estimate)
```

    ## # A tibble: 1,809 × 8
    ##    Vaccine   `Geography Type` Geography  Surve…¹ Dimen…² Dimen…³ Estim…⁴ Sampl…⁵
    ##    <chr>     <chr>            <chr>        <int> <chr>   <chr>     <dbl>   <dbl>
    ##  1 Influenza States           Alaska        2012 Age     >=18 Y…    49.2     852
    ##  2 Influenza States           Arkansas      2012 Age     >=18 Y…    46.6     756
    ##  3 Influenza States           Colorado      2012 Age     >=18 Y…    56.1    1170
    ##  4 Influenza States           Delaware      2012 Age     >=18 Y…    41.6     981
    ##  5 Influenza States           Georgia       2012 Age     >=18 Y…    33.6    1007
    ##  6 Influenza States           Hawaii        2012 Age     >=18 Y…    42      1385
    ##  7 Influenza States           Illinois      2012 Age     >=18 Y…    49.1    1037
    ##  8 Influenza States           Maine         2012 Age     >=18 Y…    53       654
    ##  9 Influenza States           Maryland      2012 Age     >=18 Y…    47.9     906
    ## 10 Influenza States           Massachus…    2012 Age     >=18 Y…    66.1    1456
    ## # … with 1,799 more rows, and abbreviated variable names
    ## #   ¹​`Survey Year_Influenza Season`, ²​`Dimension Type`, ³​Dimension, ⁴​Estimate,
    ## #   ⁵​`Sample Size`
    ## # ℹ Use `print(n = ...)` to see more rows

``` r
vaxdataDT<-data.table(vaxdata1)
is.data.table(vaxdataDT)
```

    ## [1] TRUE

``` r
vaxdataDT<-vaxdataDT %>% rename(Year="Survey Year_Influenza Season", Geo_Type="Geography Type", Age_Group="Dimension", Percent_Vaccinated="Estimate")
```

\#\`\`\`{r, examine variable of interest (% vaccinated) for implausible
values}

\`\`\`
