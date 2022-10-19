Midterm
================
CB
2022-10-19

## **Title: Influenza Vaccine Uptake by Region and Age Group from 2012-2019 in the United States**

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
Vaccination_Coverage_among_Pregnant_Women <- read_csv("C:/Users/clair/Desktop/PM566/Vaccination_Coverage_among_Pregnant_Women.csv")
```

    ## Rows: 3621 Columns: 9
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (7): Vaccine, Geography_Type, Geography_name, Dimension Type, Dimension,...
    ## dbl (2): Survey_Year_or Flu_Season, Sample_Size
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
mydata<-Vaccination_Coverage_among_Pregnant_Women
dim(mydata)
```

    ## [1] 3621    9

``` r
head(mydata)
```

    ## # A tibble: 6 × 9
    ##   Vaccine   Geography_…¹ Geogr…² Surve…³ Dimen…⁴ Dimen…⁵ Estim…⁶ CI_95…⁷ Sampl…⁸
    ##   <chr>     <chr>        <chr>     <dbl> <chr>   <chr>   <chr>   <chr>     <dbl>
    ## 1 Influenza States       Alaska     2012 Age     ≥18 Ye… 49.2    45.3 t…     852
    ## 2 Influenza States       Arkans…    2012 Age     ≥18 Ye… 46.6    40.7 t…     756
    ## 3 Influenza States       Colora…    2012 Age     ≥18 Ye… 56.1    52.1 t…    1170
    ## 4 Influenza States       Delawa…    2012 Age     ≥18 Ye… 41.6    38.4 t…     981
    ## 5 Influenza States       Georgia    2012 Age     ≥18 Ye… 33.6    29.6 t…    1007
    ## 6 Influenza States       Hawaii     2012 Age     ≥18 Ye… 42      38.7 t…    1385
    ## # … with abbreviated variable names ¹​Geography_Type, ²​Geography_name,
    ## #   ³​`Survey_Year_or Flu_Season`, ⁴​`Dimension Type`, ⁵​Dimension,
    ## #   ⁶​Estimate_Percent, ⁷​CI_95_percent, ⁸​Sample_Size

``` r
tail(mydata)
```

    ## # A tibble: 6 × 9
    ##   Vaccine Geography_Type Geogr…¹ Surve…² Dimen…³ Dimen…⁴ Estim…⁵ CI_95…⁶ Sampl…⁷
    ##   <chr>   <chr>          <chr>     <dbl> <chr>   <chr>   <chr>   <chr>     <dbl>
    ## 1 Tdap    National       United…    2019 Race/E… White,… 80.1    79.0 t…   11702
    ## 2 Tdap    States         Utah       2019 Race/E… White,… 82.7    79.6 t…    1192
    ## 3 Tdap    States         Vermont    2019 Race/E… White,… 89      86.4 t…     675
    ## 4 Tdap    States         Virgin…    2019 Race/E… White,… 78.3    71.9 t…     540
    ## 5 Tdap    States         Washin…    2019 Race/E… White,… 84.3    80.2 t…     378
    ## 6 Tdap    States         Wiscon…    2019 Race/E… White,… 78.4    72.6 t…     270
    ## # … with abbreviated variable names ¹​Geography_name,
    ## #   ²​`Survey_Year_or Flu_Season`, ³​`Dimension Type`, ⁴​Dimension,
    ## #   ⁵​Estimate_Percent, ⁶​CI_95_percent, ⁷​Sample_Size

``` r
unique(mydata$Vaccine)
```

    ## [1] "Influenza" "Tdap"

``` r
unique(mydata$Geography_Type)
```

    ## [1] "States"   "National"

``` r
unique(mydata$Geography_name)
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
