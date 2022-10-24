Midterm
================
CB
2022-10-23

# **Title: Influenza Vaccine Uptake by Region and Age Group from 2012-2019 in the United States**

### **Introduction: Pregnant women and their newborns are at higher risk for severe illness from Influenza virus infection. Influenza during pregnancy can lead to severe maternal respiratory illness requiring hospitalization. It can also be a serious condition for infants (babies under 1 year of age), especially during the neonatal period (first 30 days of life) and for those with pre-existing respiratory conditions such as bronchopulmonary dysplasia. The yearly influenza vaccine has a long track record of safety and efficacy during pregnancy and is recommended by the Centers for Disease Control (CDC) for all pregnant women (Ref). Despite this recommendation by the CDC and the American College of Obstetrics, many women choose not to receive the vaccination during pregnancy. The objective of this qualitative data analysis is two fold, first to examine factors associated with low vaccine uptake. Specifically, age group and location. Second, to examine these trends over time to see whether uptake is increasing or decreasing. Identifying those pregnant women less likely to get vaccinated can help inform where efforts to promote vaccine utilization are needed most.**

### **Methods: This data was acquired from the Centers for Disease Control website (<https://data.cdc.gov/browse?category=Pregnancy+%26+Vaccination>). Data was downloaded as a comma separated variable file directly from the website. This data included the years 2012-2019 and data for Influenza as well as Tdap was included. I only wanted to look at Influenza vaccination so this data was selected for. All 50 states plus Puerto Rico and District of Columbia were in the dataset. As I only wanted to examine the 50 states, I removed data for Puerto Rico and District of Columbia. Missingness was examined and there were found to be only 15 out of 1,809 observation missing. As this is less than 1%, missing data was removed from the dataset. A region variable was created using regions specified on the CDC website. Duplicate rows were examined for and removed. Figures were made include boxplots and bargraphs in order to visualize trends in data and make conclusions about the findings. Tables were also made in order to show findings with numeric values included. Data analysis was done using “R”, an open source data analysis tool (R Core Team (2018). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria.URL <https://www.R-project.org/>.)**

#### Preliminary Results: First we examined the vaccination rates by age group with three groups: Women 18-24 years old, 24-34 years old and 35 years old or greater (Figure1). This was graphed over time between the years 2012-2019. We can see that wOmen 35 years old and above tend to have higher vaccination rates and those aged 18-24 years tend to have the lowest. This suggests that as women get older they are more likely to get the influenza vaccine during pregnancy. It appears that comparing 2012 to 2019 that the gap in vaccination rate between age groups is shrinking, with the years 2018 and 2019 having nearly equal rates.

![](Midterm1_files/figure-gfm/create%20first%20table-1.png)<!-- -->

#### Figure 1. This figure demonstrates the change in Influenza vaccination uptake among pregnant women in the U.S. over time by age group. The timeframe is between the years 2012 and 2019.

#### Next, we examined Influenza vaccination rates by region, comparing the year 2012 to the year 2019 (Figure 2). We see that in both 2012 and 2019 the Southern U.S. has had the lowest vaccination rates. However this vaccination rate gap has grown considerably over time with rates far below the rest of the country by 2019. In 2012 the West had the highest vaccination rate but over time this has gone down relative to the other regions and in 2019 it was the Northeast with the highest rate.

![](Midterm1_files/figure-gfm/compare%20vaccine%20rates%20by%20region%20over%20time-1.png)<!-- -->

#### Figure 2. This boxplot figure shows Influenza vaccination rates as a percentage among pregnant women in the United States by region in the year 2012 versus 2019.

#### In order to examine the data in a more numeric way we next looked at the change in vaccination rates between the years 2012 and 2019 to see which states had the biggest changes (Table 1). The states of New York and Wyoming had the largest increase in vaccine rate, both going up 26.5% between 2012 and 2019.

| State        | Year_2012 | Year_2019 | Change |
|:-------------|:---------:|:---------:|:------:|
| New York     |   37.8    |   64.3    |  26.5  |
| Wyoming      |   39.1    |   65.6    |  26.5  |
| Hawaii       |   42.0    |   64.6    |  22.6  |
| Rhode Island |   60.4    |   82.2    |  21.8  |
| Delaware     |   41.6    |   62.7    |  21.1  |
| Nebraska     |   58.8    |   77.9    |  19.1  |
| Missouri     |   45.5    |   64.3    |  18.8  |
| Colorado     |   56.1    |   74.8    |  18.7  |
| Maryland     |   47.9    |   66.1    |  18.2  |
| New Jersey   |   38.6    |   56.8    |  18.2  |

Table 1. Influenza Vaccination Among Pregnant Women - Rate Change by
State in the U.S.

## Conclusion: In examining this data about Influenza vaccination among pregnant women we found that overall, the vaccine rate is increasing in the United States. In the past younger women were vaccinated at lower rates than older women but this gap has been all but closed recently. We also see that in examining by region that the Southern U.S. has lower vaccination rate than the rest of the country. This gap has only widened over time with this region lagging significantly behind. Overall this data indicates that efforts to improve Influenza vaccine uptake by pregnant women in the U.S would benefit from targeting the Southern U.S. and that all age groups should be included in these efforts.
