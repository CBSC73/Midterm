Midterm
================
CB
2022-10-19

## **Title: Influenza Vaccine Uptake by Region and Age Group from 2012-2019 in the United States**

# \*\*Introduction: Pregnant women and newborns are at higher risk for severe illness from Influenza virus infection(Ref). Influenza during pregnancy can lead to severe maternal respiratory illness requiring hospitalization. It can also be a serious condition for infants (babies under 1 year of age), especially during the neonatal period (first 30 days of life) and for those with pre-existing respiratory conditions such as bronchopulmonary dysplasia (Ref). The yearly influenza vaccine has a long track record of safety and efficacy during pregnancy and is recommended by the Centers for Disease Control (CDC) for all pregnant women (Ref). Despite this recommendation, only approximately 50% of women receive the influenza vaccine during pregnancy (ref).The objective of this qualitative data analysis is two fold, first to examine factors associated with low vaccine uptake. Specifically, age group, location, and ethnicity. And second, to examine these trends over time to see whether uptake is increasing or decreasing. Identifying those pregnant women less likely to get vaccinated can help inform where efforts to promote vaccine utilization are needed most.

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
Vaccination_Coverage_among_Pregnant_Women <- read_csv("C:/Users/clair/Desktop/PM566/Vaccination_Coverage_among_Pregnant_Women.csv", 
    col_types = cols(Estimate_Percent = col_number()))
```

    ## Warning: One or more parsing issues, see `problems()` for details

``` r
View(Vaccination_Coverage_among_Pregnant_Women)
```

``` r
mydata<-Vaccination_Coverage_among_Pregnant_Women
dim(mydata)
```

    ## [1] 3621    9

``` r
setDT(mydata)
```

``` r
head(mydata)
```

    ##      Vaccine Geography_Type Geography_name Year Dimension Type Dimension
    ## 1: Influenza         States         Alaska 2012            Age ≥18 Years
    ## 2: Influenza         States       Arkansas 2012            Age ≥18 Years
    ## 3: Influenza         States       Colorado 2012            Age ≥18 Years
    ## 4: Influenza         States       Delaware 2012            Age ≥18 Years
    ## 5: Influenza         States        Georgia 2012            Age ≥18 Years
    ## 6: Influenza         States         Hawaii 2012            Age ≥18 Years
    ##    Estimate_Percent CI_95_percent Sample_Size
    ## 1:             49.2  45.3 to 53.1         852
    ## 2:             46.6  40.7 to 52.5         756
    ## 3:             56.1  52.1 to 60.0        1170
    ## 4:             41.6  38.4 to 44.8         981
    ## 5:             33.6  29.6 to 37.7        1007
    ## 6:             42.0  38.7 to 45.4        1385

``` r
tail(mydata)
```

    ##    Vaccine Geography_Type Geography_name Year Dimension Type
    ## 1:    Tdap       National  United States 2019 Race/Ethnicity
    ## 2:    Tdap         States           Utah 2019 Race/Ethnicity
    ## 3:    Tdap         States        Vermont 2019 Race/Ethnicity
    ## 4:    Tdap         States       Virginia 2019 Race/Ethnicity
    ## 5:    Tdap         States     Washington 2019 Race/Ethnicity
    ## 6:    Tdap         States      Wisconsin 2019 Race/Ethnicity
    ##              Dimension Estimate_Percent CI_95_percent Sample_Size
    ## 1: White, Non-Hispanic             80.1  79.0 to 81.2       11702
    ## 2: White, Non-Hispanic             82.7  79.6 to 85.5        1192
    ## 3: White, Non-Hispanic             89.0  86.4 to 91.3         675
    ## 4: White, Non-Hispanic             78.3  71.9 to 83.8         540
    ## 5: White, Non-Hispanic             84.3  80.2 to 87.9         378
    ## 6: White, Non-Hispanic             78.4  72.6 to 83.5         270

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

``` r
unique(mydata$Year)
```

    ## [1] 2012 2013 2014 2015 2016 2017 2018 2019

``` r
unique(mydata$"Dimension Type")
```

    ## [1] "Age"            "Race/Ethnicity"

``` r
unique(mydata$Dimension)
```

    ## [1] "≥18 Years"                            
    ## [2] "18-24 Years"                          
    ## [3] "25-34 Years"                          
    ## [4] "≥35 Years"                            
    ## [5] "Black, Non-Hispanic"                  
    ## [6] "Hispanic"                             
    ## [7] "Other or Multiple Races, Non-Hispanic"
    ## [8] "White, Non-Hispanic"

``` r
colSums(is.na(mydata))
```

    ##          Vaccine   Geography_Type   Geography_name             Year 
    ##                0                0                0                0 
    ##   Dimension Type        Dimension Estimate_Percent    CI_95_percent 
    ##                0                0              364                0 
    ##      Sample_Size 
    ##              173

``` r
summary(mydata$Estimate_Percent)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##    5.20   51.20   61.20   60.18   70.90   93.70     364

``` r
summary(mydata$Year)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    2012    2013    2016    2016    2018    2019

``` r
explore <-subset(mydata, is.na(mydata$Estimate_Percent))
dim(explore)
```

    ## [1] 364   9

``` r
table(explore$Vaccine)
```

    ## 
    ## Influenza      Tdap 
    ##       274        90

``` r
table(explore$Year)
```

    ## 
    ## 2012 2013 2014 2015 2016 2017 2018 2019 
    ##   68   41   28   39   35   44   55   54

``` r
table(explore$Geography_name)
```

    ## 
    ##              Alabama               Alaska             Arkansas 
    ##                    5                   12                   22 
    ##             Colorado             Delaware District of Columbia 
    ##                   20                    2                    2 
    ##              Florida              Georgia               Hawaii 
    ##                    1                    7                   10 
    ##             Illinois                 Iowa               Kansas 
    ##                    1                   11                    4 
    ##             Kentucky            Louisiana                Maine 
    ##                    6                   11                   27 
    ##             Michigan            Minnesota          Mississippi 
    ##                    5                    2                    8 
    ##             Missouri              Montana        New Hampshire 
    ##                   20                    9                   34 
    ##           New Mexico             New York         North Dakota 
    ##                   10                    2                    6 
    ##     NY-Rest of state                 Ohio             Oklahoma 
    ##                   18                    2                   10 
    ##         Pennsylvania          Puerto Rico            Tennessee 
    ##                    9                    8                   10 
    ##                 Utah             Virginia        West Virginia 
    ##                   16                    5                   24 
    ##              Wyoming 
    ##                   25

``` r
table(explore$Dimension)
```

    ## 
    ##                             ≥35 Years                           18-24 Years 
    ##                                    14                                     1 
    ##                   Black, Non-Hispanic                              Hispanic 
    ##                                   127                                    88 
    ## Other or Multiple Races, Non-Hispanic                   White, Non-Hispanic 
    ##                                   131                                     3
