---
title: "Assignment01"
author: "Audrey Omidsalar"
date: "9/24/2021"
output:
  html_document:
    toc: yes
    toc_float: yes
    keep_md: yes
---



## Step 1
### Download the 2004 and 2019 EPA Air Quality PM2.5 data from all sites in California, and check for any data issues
#### Reading in the 2004 dataset as `data2004` and the 2019 dataset as `data2019`

```r
data2004 <- data.table::fread("ad_viz_plotval_data_2004.csv")
data2019 <- data.table::fread("ad_viz_plotval_data_2019.csv")
```

#### Checking the dimensions of each dataset
The 2004 dataset has 19,233 rows and 20 columns. The 2019 dataset has 53,086 rows and 20 columns.

```r
dim(data2004)
```

```
## [1] 19233    20
```

```r
dim(data2019)
```

```
## [1] 53086    20
```
#### Checking headers and footers of `data2004`

```r
head(data2004)
```

```
##          Date Source  Site ID POC Daily Mean PM2.5 Concentration    UNITS
## 1: 01/01/2004    AQS 60010007   1                            8.9 ug/m3 LC
## 2: 01/02/2004    AQS 60010007   1                           12.2 ug/m3 LC
## 3: 01/03/2004    AQS 60010007   1                           16.5 ug/m3 LC
## 4: 01/04/2004    AQS 60010007   1                           19.5 ug/m3 LC
## 5: 01/05/2004    AQS 60010007   1                           11.5 ug/m3 LC
## 6: 01/06/2004    AQS 60010007   1                           32.5 ug/m3 LC
##    DAILY_AQI_VALUE Site Name DAILY_OBS_COUNT PERCENT_COMPLETE
## 1:              37 Livermore               1              100
## 2:              51 Livermore               1              100
## 3:              60 Livermore               1              100
## 4:              67 Livermore               1              100
## 5:              48 Livermore               1              100
## 6:              94 Livermore               1              100
##    AQS_PARAMETER_CODE                     AQS_PARAMETER_DESC CBSA_CODE
## 1:              88101               PM2.5 - Local Conditions     41860
## 2:              88502 Acceptable PM2.5 AQI & Speciation Mass     41860
## 3:              88502 Acceptable PM2.5 AQI & Speciation Mass     41860
## 4:              88502 Acceptable PM2.5 AQI & Speciation Mass     41860
## 5:              88502 Acceptable PM2.5 AQI & Speciation Mass     41860
## 6:              88502 Acceptable PM2.5 AQI & Speciation Mass     41860
##                            CBSA_NAME STATE_CODE      STATE COUNTY_CODE  COUNTY
## 1: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 2: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 3: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 4: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 5: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 6: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
##    SITE_LATITUDE SITE_LONGITUDE
## 1:      37.68753      -121.7842
## 2:      37.68753      -121.7842
## 3:      37.68753      -121.7842
## 4:      37.68753      -121.7842
## 5:      37.68753      -121.7842
## 6:      37.68753      -121.7842
```

```r
tail(data2004)
```

```
##          Date Source  Site ID POC Daily Mean PM2.5 Concentration    UNITS
## 1: 12/14/2004    AQS 61131003   1                             11 ug/m3 LC
## 2: 12/17/2004    AQS 61131003   1                             16 ug/m3 LC
## 3: 12/20/2004    AQS 61131003   1                             17 ug/m3 LC
## 4: 12/23/2004    AQS 61131003   1                              9 ug/m3 LC
## 5: 12/26/2004    AQS 61131003   1                             24 ug/m3 LC
## 6: 12/29/2004    AQS 61131003   1                              9 ug/m3 LC
##    DAILY_AQI_VALUE            Site Name DAILY_OBS_COUNT PERCENT_COMPLETE
## 1:              46 Woodland-Gibson Road               1              100
## 2:              59 Woodland-Gibson Road               1              100
## 3:              61 Woodland-Gibson Road               1              100
## 4:              38 Woodland-Gibson Road               1              100
## 5:              76 Woodland-Gibson Road               1              100
## 6:              38 Woodland-Gibson Road               1              100
##    AQS_PARAMETER_CODE       AQS_PARAMETER_DESC CBSA_CODE
## 1:              88101 PM2.5 - Local Conditions     40900
## 2:              88101 PM2.5 - Local Conditions     40900
## 3:              88101 PM2.5 - Local Conditions     40900
## 4:              88101 PM2.5 - Local Conditions     40900
## 5:              88101 PM2.5 - Local Conditions     40900
## 6:              88101 PM2.5 - Local Conditions     40900
##                                  CBSA_NAME STATE_CODE      STATE COUNTY_CODE
## 1: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 2: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 3: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 4: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 5: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 6: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
##    COUNTY SITE_LATITUDE SITE_LONGITUDE
## 1:   Yolo      38.66121      -121.7327
## 2:   Yolo      38.66121      -121.7327
## 3:   Yolo      38.66121      -121.7327
## 4:   Yolo      38.66121      -121.7327
## 5:   Yolo      38.66121      -121.7327
## 6:   Yolo      38.66121      -121.7327
```
#### Checking headers and footers of `data2019`

```r
head(data2019)
```

```
##          Date Source  Site ID POC Daily Mean PM2.5 Concentration    UNITS
## 1: 01/01/2019    AQS 60010007   3                            5.7 ug/m3 LC
## 2: 01/02/2019    AQS 60010007   3                           11.9 ug/m3 LC
## 3: 01/03/2019    AQS 60010007   3                           20.1 ug/m3 LC
## 4: 01/04/2019    AQS 60010007   3                           28.8 ug/m3 LC
## 5: 01/05/2019    AQS 60010007   3                           11.2 ug/m3 LC
## 6: 01/06/2019    AQS 60010007   3                            2.7 ug/m3 LC
##    DAILY_AQI_VALUE Site Name DAILY_OBS_COUNT PERCENT_COMPLETE
## 1:              24 Livermore               1              100
## 2:              50 Livermore               1              100
## 3:              68 Livermore               1              100
## 4:              86 Livermore               1              100
## 5:              47 Livermore               1              100
## 6:              11 Livermore               1              100
##    AQS_PARAMETER_CODE       AQS_PARAMETER_DESC CBSA_CODE
## 1:              88101 PM2.5 - Local Conditions     41860
## 2:              88101 PM2.5 - Local Conditions     41860
## 3:              88101 PM2.5 - Local Conditions     41860
## 4:              88101 PM2.5 - Local Conditions     41860
## 5:              88101 PM2.5 - Local Conditions     41860
## 6:              88101 PM2.5 - Local Conditions     41860
##                            CBSA_NAME STATE_CODE      STATE COUNTY_CODE  COUNTY
## 1: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 2: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 3: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 4: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 5: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 6: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
##    SITE_LATITUDE SITE_LONGITUDE
## 1:      37.68753      -121.7842
## 2:      37.68753      -121.7842
## 3:      37.68753      -121.7842
## 4:      37.68753      -121.7842
## 5:      37.68753      -121.7842
## 6:      37.68753      -121.7842
```

```r
tail(data2019)
```

```
##          Date Source  Site ID POC Daily Mean PM2.5 Concentration    UNITS
## 1: 11/11/2019    AQS 61131003   1                           13.5 ug/m3 LC
## 2: 11/17/2019    AQS 61131003   1                           18.1 ug/m3 LC
## 3: 11/29/2019    AQS 61131003   1                           12.5 ug/m3 LC
## 4: 12/17/2019    AQS 61131003   1                           23.8 ug/m3 LC
## 5: 12/23/2019    AQS 61131003   1                            1.0 ug/m3 LC
## 6: 12/29/2019    AQS 61131003   1                            9.1 ug/m3 LC
##    DAILY_AQI_VALUE            Site Name DAILY_OBS_COUNT PERCENT_COMPLETE
## 1:              54 Woodland-Gibson Road               1              100
## 2:              64 Woodland-Gibson Road               1              100
## 3:              52 Woodland-Gibson Road               1              100
## 4:              76 Woodland-Gibson Road               1              100
## 5:               4 Woodland-Gibson Road               1              100
## 6:              38 Woodland-Gibson Road               1              100
##    AQS_PARAMETER_CODE       AQS_PARAMETER_DESC CBSA_CODE
## 1:              88101 PM2.5 - Local Conditions     40900
## 2:              88101 PM2.5 - Local Conditions     40900
## 3:              88101 PM2.5 - Local Conditions     40900
## 4:              88101 PM2.5 - Local Conditions     40900
## 5:              88101 PM2.5 - Local Conditions     40900
## 6:              88101 PM2.5 - Local Conditions     40900
##                                  CBSA_NAME STATE_CODE      STATE COUNTY_CODE
## 1: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 2: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 3: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 4: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 5: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
## 6: Sacramento--Roseville--Arden-Arcade, CA          6 California         113
##    COUNTY SITE_LATITUDE SITE_LONGITUDE
## 1:   Yolo      38.66121      -121.7327
## 2:   Yolo      38.66121      -121.7327
## 3:   Yolo      38.66121      -121.7327
## 4:   Yolo      38.66121      -121.7327
## 5:   Yolo      38.66121      -121.7327
## 6:   Yolo      38.66121      -121.7327
```
#### Checking variable names and variable types of both datasets.

```r
summary(data2004)
```

```
##      Date              Source             Site ID              POC        
##  Length:19233       Length:19233       Min.   :60010007   Min.   : 1.000  
##  Class :character   Class :character   1st Qu.:60370002   1st Qu.: 1.000  
##  Mode  :character   Mode  :character   Median :60658001   Median : 1.000  
##                                        Mean   :60588026   Mean   : 1.816  
##                                        3rd Qu.:60750006   3rd Qu.: 2.000  
##                                        Max.   :61131003   Max.   :12.000  
##                                                                           
##  Daily Mean PM2.5 Concentration    UNITS           DAILY_AQI_VALUE 
##  Min.   : -0.10                 Length:19233       Min.   :  0.00  
##  1st Qu.:  6.00                 Class :character   1st Qu.: 25.00  
##  Median : 10.10                 Mode  :character   Median : 42.00  
##  Mean   : 13.13                                    Mean   : 46.32  
##  3rd Qu.: 16.30                                    3rd Qu.: 60.00  
##  Max.   :251.00                                    Max.   :301.00  
##                                                                    
##   Site Name         DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE
##  Length:19233       Min.   :1       Min.   :100      Min.   :88101     
##  Class :character   1st Qu.:1       1st Qu.:100      1st Qu.:88101     
##  Mode  :character   Median :1       Median :100      Median :88101     
##                     Mean   :1       Mean   :100      Mean   :88267     
##                     3rd Qu.:1       3rd Qu.:100      3rd Qu.:88502     
##                     Max.   :1       Max.   :100      Max.   :88502     
##                                                                        
##  AQS_PARAMETER_DESC   CBSA_CODE      CBSA_NAME           STATE_CODE
##  Length:19233       Min.   :12540   Length:19233       Min.   :6   
##  Class :character   1st Qu.:31080   Class :character   1st Qu.:6   
##  Mode  :character   Median :40140   Mode  :character   Median :6   
##                     Mean   :35328                      Mean   :6   
##                     3rd Qu.:41860                      3rd Qu.:6   
##                     Max.   :49700                      Max.   :6   
##                     NA's   :1253                                   
##     STATE            COUNTY_CODE        COUNTY          SITE_LATITUDE  
##  Length:19233       Min.   :  1.00   Length:19233       Min.   :32.63  
##  Class :character   1st Qu.: 37.00   Class :character   1st Qu.:34.07  
##  Mode  :character   Median : 65.00   Mode  :character   Median :36.48  
##                     Mean   : 58.63                      Mean   :36.23  
##                     3rd Qu.: 75.00                      3rd Qu.:38.10  
##                     Max.   :113.00                      Max.   :41.71  
##                                                                        
##  SITE_LONGITUDE  
##  Min.   :-124.2  
##  1st Qu.:-121.6  
##  Median :-119.3  
##  Mean   :-119.7  
##  3rd Qu.:-117.9  
##  Max.   :-115.5  
## 
```

```r
summary(data2019)
```

```
##      Date              Source             Site ID              POC        
##  Length:53086       Length:53086       Min.   :60010007   Min.   : 1.000  
##  Class :character   Class :character   1st Qu.:60310004   1st Qu.: 1.000  
##  Mode  :character   Mode  :character   Median :60612003   Median : 3.000  
##                                        Mean   :60565291   Mean   : 2.562  
##                                        3rd Qu.:60771002   3rd Qu.: 3.000  
##                                        Max.   :61131003   Max.   :21.000  
##                                                                           
##  Daily Mean PM2.5 Concentration    UNITS           DAILY_AQI_VALUE 
##  Min.   : -2.200                Length:53086       Min.   :  0.00  
##  1st Qu.:  4.000                Class :character   1st Qu.: 17.00  
##  Median :  6.500                Mode  :character   Median : 27.00  
##  Mean   :  7.734                                   Mean   : 30.56  
##  3rd Qu.:  9.900                                   3rd Qu.: 41.00  
##  Max.   :120.900                                   Max.   :185.00  
##                                                                    
##   Site Name         DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE
##  Length:53086       Min.   :1       Min.   :100      Min.   :88101     
##  Class :character   1st Qu.:1       1st Qu.:100      1st Qu.:88101     
##  Mode  :character   Median :1       Median :100      Median :88101     
##                     Mean   :1       Mean   :100      Mean   :88214     
##                     3rd Qu.:1       3rd Qu.:100      3rd Qu.:88502     
##                     Max.   :1       Max.   :100      Max.   :88502     
##                                                                        
##  AQS_PARAMETER_DESC   CBSA_CODE      CBSA_NAME           STATE_CODE
##  Length:53086       Min.   :12540   Length:53086       Min.   :6   
##  Class :character   1st Qu.:31080   Class :character   1st Qu.:6   
##  Mode  :character   Median :40140   Mode  :character   Median :6   
##                     Mean   :35841                      Mean   :6   
##                     3rd Qu.:41860                      3rd Qu.:6   
##                     Max.   :49700                      Max.   :6   
##                     NA's   :4181                                   
##     STATE            COUNTY_CODE        COUNTY          SITE_LATITUDE  
##  Length:53086       Min.   :  1.00   Length:53086       Min.   :32.58  
##  Class :character   1st Qu.: 31.00   Class :character   1st Qu.:34.14  
##  Mode  :character   Median : 61.00   Mode  :character   Median :36.63  
##                     Mean   : 56.39                      Mean   :36.35  
##                     3rd Qu.: 77.00                      3rd Qu.:37.97  
##                     Max.   :113.00                      Max.   :41.76  
##                                                                        
##  SITE_LONGITUDE  
##  Min.   :-124.2  
##  1st Qu.:-121.6  
##  Median :-119.8  
##  Mean   :-119.8  
##  3rd Qu.:-118.1  
##  Max.   :-115.5  
## 
```
Some of the column names have spaces, and some of the key variables can be renamed to be more succinct.

## Step 2
### Combine the two years of data into one data frame. Use the Date variable to create a new column for year, which will serve as an identifier. Change the names of the key variables so that they are easier to refer to in your code.

```r
##add column with year number in the two datasets
data2004[, year := 2004]
data2019[, year := 2019]
##combine the datasets
combined <- rbind(data2004, data2019)
##change column names
setnames(combined, "Daily Mean PM2.5 Concentration", "PM2.5")
setnames(combined,"Site ID", "Site_ID")
setnames(combined, "Site Name", "Site_Name")
setnames(combined, "SITE_LATITUDE", "lat")
setnames(combined, "SITE_LONGITUDE", "lon")
```
## Step 3
### Create a basic map in leaflet() that shows the locations of the sites (make sure to use different colors for each year). Summarize the spatial distribution of the monitoring sites.
There are more monitoring sites in 2019 compared to in 2004, which makes sense given the number of observations in the two initial datasets. The monitoring sites seem to be mostly clustered around major cities: in southern California, there are more monitoring sites along the coast then in the inland regions; in central California, there is a cluster of monitoring sites near Fresno; in northern California, there are clusters in the Bay Area and other larger cities (Sacramento, Eureka). Overall, there is a pretty fair distribution of monitoring sites across the state, with the empty regions corresponding to areas that are likely largely uninhabited.

```r
year.pal <- colorFactor(c('purple', 'pink'), domain = combined$year)
leaflet(combined) %>%
  addProviderTiles('CartoDB.Positron') %>%
  addCircles(lat = ~lat, lng=~lon,
     label = ~paste0(round(year,2), 'year'), color = ~ year.pal(year),
     opacity = 1, fillOpacity = 1, radius = 500) %>%
     addLegend('bottomleft', pal=year.pal, values=combined$year,
          title='Year', opacity=1)
```

```{=html}
<div id="htmlwidget-076b02762821bd61deb6" style="width:672px;height:480px;" class="leaflet html-widget"></div>
```
## Step 4
### Check for any missing or implausible values of PM2.5 in the combined dataset. Explore the proportions of each and provide a summary of any temporal patterns you see in these observations
The maximum is quite high in comparison to the median, which suggests there are outlier(s) in this dataset. Many of the highest PM2.5 values seem to be coming from the "Yosemite NP-Yosemite Village Visitor Center" Site and occurred around the same time -- perhaps there was a natural disaster at that time.

The negative PM2.5 values do not make sense, so they will be removed. The proportion of negative PM2.5 values over the total amount of PM2.5 data is 0.0039. There are no NA values for PM2.5 in this dataset.

```r
summary(combined$PM2.5)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  -2.200   4.400   7.200   9.168  11.300 251.000
```

```r
ggplot(combined, mapping=aes(x=1, y=PM2.5)) + 
  geom_violin() + 
  facet_grid(~ year)
```

![](README_files/figure-html/filtering-1.png)<!-- -->

```r
combined2 <- combined[order(-PM2.5)]
head(combined2)
```

```
##          Date Source  Site_ID POC PM2.5    UNITS DAILY_AQI_VALUE
## 1: 07/18/2004    AQS 60431001   3 251.0 ug/m3 LC             301
## 2: 07/19/2004    AQS 60431001   3 170.4 ug/m3 LC             221
## 3: 07/20/2004    AQS 60431001   3 148.4 ug/m3 LC             199
## 4: 07/21/2004    AQS 60431001   3 122.5 ug/m3 LC             186
## 5: 10/11/2019    AQS 60371201   3 120.9 ug/m3 LC             185
## 6: 07/15/2004    AQS 60431001   3 110.4 ug/m3 LC             179
##                                     Site_Name DAILY_OBS_COUNT PERCENT_COMPLETE
## 1: Yosemite NP-Yosemite Village Vistor Center               1              100
## 2: Yosemite NP-Yosemite Village Vistor Center               1              100
## 3: Yosemite NP-Yosemite Village Vistor Center               1              100
## 4: Yosemite NP-Yosemite Village Vistor Center               1              100
## 5:                                     Reseda               1              100
## 6: Yosemite NP-Yosemite Village Vistor Center               1              100
##    AQS_PARAMETER_CODE                     AQS_PARAMETER_DESC CBSA_CODE
## 1:              88502 Acceptable PM2.5 AQI & Speciation Mass        NA
## 2:              88502 Acceptable PM2.5 AQI & Speciation Mass        NA
## 3:              88502 Acceptable PM2.5 AQI & Speciation Mass        NA
## 4:              88502 Acceptable PM2.5 AQI & Speciation Mass        NA
## 5:              88502 Acceptable PM2.5 AQI & Speciation Mass     31080
## 6:              88502 Acceptable PM2.5 AQI & Speciation Mass        NA
##                             CBSA_NAME STATE_CODE      STATE COUNTY_CODE
## 1:                                             6 California          43
## 2:                                             6 California          43
## 3:                                             6 California          43
## 4:                                             6 California          43
## 5: Los Angeles-Long Beach-Anaheim, CA          6 California          37
## 6:                                             6 California          43
##         COUNTY      lat       lon year
## 1:    Mariposa 37.74871 -119.5871 2004
## 2:    Mariposa 37.74871 -119.5871 2004
## 3:    Mariposa 37.74871 -119.5871 2004
## 4:    Mariposa 37.74871 -119.5871 2004
## 5: Los Angeles 34.19925 -118.5328 2019
## 6:    Mariposa 37.74871 -119.5871 2004
```

```r
dim(combined[PM2.5<0])[1]/dim(combined)[1]
```

```
## [1] 0.003913218
```

```r
dim(combined[is.na(PM2.5)])
```

```
## [1]  0 21
```

```r
combined3 <- combined[PM2.5>=0]
data2004_v2 <- data2004[`Daily Mean PM2.5 Concentration`>=0]
data2019_v2 <- data2019[`Daily Mean PM2.5 Concentration` >=0]
```
## Step 5
### Explore the main question of interest at three different spatial levels (state, county, site in Los Angeles).
### Question of Interest: Have daily concentrations of PM2.5 (particulate matter air pollution with aerodynamic diameter less than 2.5μm) decreased in California over the last 15 years (from 2004 to 2019)?
### State Level
These summary statistics of "Daily Mean PM2.5 Concentration" as well as the "Daily AQI Value" of each year's data show that both the mean daily PM2.5 concentration and the mean daily AQI value have decreased from 2004 to 2019 (13.13 to 7.78 and 46.33 to 30.72, accordingly); the same relationship is seen with the median PM2.5 concentration and AQI value(10.10 to 6.50 and 42.0 to 72.0, accordingly). The AQI value is the air quality index score, which is an overall indicator of air quality due to pollutants. I have included this in order to gain information about the changes in air quality overall across these two years.

```r
summary(data2004_v2$`Daily Mean PM2.5 Concentration`)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    0.00    6.00   10.10   13.13   16.30  251.00
```

```r
summary(data2004_v2$DAILY_AQI_VALUE)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    0.00   25.00   42.00   46.33   60.00  301.00
```

```r
summary(data2019_v2$`Daily Mean PM2.5 Concentration`)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    0.00    4.00    6.50    7.78   10.00  120.90
```

```r
summary(data2019_v2$DAILY_AQI_VALUE)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    0.00   17.00   27.00   30.72   42.00  185.00
```
Here are boxplots for the daily Mean PM2.5 Concentration per Year. 2004 has a greater IQR than 2019, and 2004 has outliers with higher PM2.5 concentrations (though both years have many outliers), which are likely contributing to the higher overall average PM2.5 value for this year.

```r
ggplot(combined3) +
  geom_boxplot(mapping=aes(x=year, y = PM2.5, group=year)) +
  labs(title = "Statewide PM2.5 Concentrations", x  = "Year", y = "Daily Mean PM2.5 Concentration")
```

![](README_files/figure-html/state boxplot-1.png)<!-- -->
The histograms of the daily mean PM2.5 concentrations for each year are skewed to the right, but the outliers are likely due to disaster events (ex. wildfires). However, the 2004 graph has higher daily mean PM2.5 concentrations, as seen on the x axes.

```r
hist(data2004_v2$`Daily Mean PM2.5 Concentration`, breaks=100)
```

![](README_files/figure-html/state hist-1.png)<!-- -->

```r
hist(data2019_v2$`Daily Mean PM2.5 Concentration`, breaks=100)
```

![](README_files/figure-html/state hist-2.png)<!-- -->

```r
## Making a data table with average PM2.5 and AQI values
combined3_avg <- combined3[, .(
  PM2.5     = mean(PM2.5, na.rm=TRUE),
  AQI       = mean(DAILY_AQI_VALUE, na.rm=TRUE), STATE, COUNTY), by = "year"]
combined3_avg
```

```
##        year     PM2.5      AQI      STATE  COUNTY
##     1: 2004 13.125889 46.32519 California Alameda
##     2: 2004 13.125889 46.32519 California Alameda
##     3: 2004 13.125889 46.32519 California Alameda
##     4: 2004 13.125889 46.32519 California Alameda
##     5: 2004 13.125889 46.32519 California Alameda
##    ---                                           
## 72032: 2019  7.779863 30.71932 California    Yolo
## 72033: 2019  7.779863 30.71932 California    Yolo
## 72034: 2019  7.779863 30.71932 California    Yolo
## 72035: 2019  7.779863 30.71932 California    Yolo
## 72036: 2019  7.779863 30.71932 California    Yolo
```
These line plots show the state-wide average PM2.5 Concentrations per year as well as the average AQI scores per year are decreasing from 2004 to 2019.

```r
#ggplot(combined3_avg) +
#  geom_point(mapping=aes(x=year, y = PM2.5), color='blue',show.legend = FALSE) +
#  geom_line(mapping=aes(x=year, y = PM2.5), color='blue',show.legend = FALSE) +
#  labs(title = "PM2.5 Averages Per Year", x  = "Year", y = "Average PM2.5 Concentration")
#ggplot(combined3_avg) +
#  geom_point(mapping=aes(x=year, y = AQI), color='red', show.legend = FALSE) +
#  geom_line(mapping=aes(x=year, y = AQI), color='red', show.legend = FALSE) +
#  labs(title = "AQI Averages Per Year", x  = "Year", y = "Average AQI")

colors <- c("Average PM2.5 Concentration" = "blue", "Average Daily AQI" = "red")
ggplot(combined3_avg) +
  geom_point(mapping=aes(x=year, y = PM2.5, color="Average PM2.5 Concentration")) +
  geom_line(mapping=aes(x=year, y = PM2.5, color='Average PM2.5 Concentration')) +
  geom_point(mapping=aes(x=year, y = AQI, color='Average Daily AQI')) +
  geom_line(mapping=aes(x=year, y = AQI, color='Average Daily AQI')) +
  labs(title = "State-Wide Mean PM2.5 and Mean AQI Values" , y = 'Value', x= "Year", color = "Legend") +
    scale_color_manual(values = colors)
```

![](README_files/figure-html/state lineplot-1.png)<!-- -->
### County-wide

```r
##Calculate average PM2.5 and AQI by County per year
county_2004 <- data2004_v2[, .(
  PM2.5     = mean(`Daily Mean PM2.5 Concentration`, na.rm=TRUE),
  AQI       = mean(DAILY_AQI_VALUE, na.rm=TRUE), STATE), by = "COUNTY"]
county_2019 <- data2019_v2[, .(
  PM2.5     = mean(`Daily Mean PM2.5 Concentration`, na.rm=TRUE),
  AQI       = mean(DAILY_AQI_VALUE, na.rm=TRUE), STATE), by = "COUNTY"]
##Combine the two datasets and add year variable
county_2004[, year := 2004]
county_2019[, year := 2019]
county_combined <- rbind(county_2004, county_2019)
```
Here, the average PM2.5 concentrations can be visualized for each county per year.

```r
unique(county_2004, by = "COUNTY")
```

```
##              COUNTY     PM2.5      AQI      STATE year
##  1:         Alameda 11.079039 41.44323 California 2004
##  2:           Butte 10.069820 37.43694 California 2004
##  3:       Calaveras  7.606557 30.63934 California 2004
##  4:          Colusa 10.049254 36.77114 California 2004
##  5:    Contra Costa 12.781467 44.65251 California 2004
##  6:       Del Norte  3.405983 14.25641 California 2004
##  7:       El Dorado  3.519531 14.36719 California 2004
##  8:          Fresno 15.455309 52.01728 California 2004
##  9:        Humboldt  8.215517 32.12069 California 2004
## 10:        Imperial 11.034973 41.87432 California 2004
## 11:            Inyo  4.557085 18.04453 California 2004
## 12:            Kern 17.104064 56.76227 California 2004
## 13:           Kings 19.654762 63.83333 California 2004
## 14:            Lake  4.468333 18.48333 California 2004
## 15:     Los Angeles 17.100134 58.76237 California 2004
## 16:           Marin  5.773333 23.56667 California 2004
## 17:        Mariposa 13.171250 41.02813 California 2004
## 18:       Mendocino  6.959016 28.65574 California 2004
## 19:          Merced 17.180000 57.58889 California 2004
## 20:            Mono  4.152486 16.62431 California 2004
## 21:        Monterey  6.940000 28.38333 California 2004
## 22:          Nevada  6.517241 26.56034 California 2004
## 23:          Orange 16.266541 57.01890 California 2004
## 24:          Placer 13.963008 50.02846 California 2004
## 25:          Plumas 11.011628 40.40698 California 2004
## 26:       Riverside 18.424356 60.08894 California 2004
## 27:      Sacramento 13.432691 47.49828 California 2004
## 28:      San Benito  4.245082 17.64754 California 2004
## 29:  San Bernardino 14.249496 48.75028 California 2004
## 30:       San Diego 13.324389 49.62404 California 2004
## 31:   San Francisco 10.782679 40.40714 California 2004
## 32:     San Joaquin 13.188525 47.45082 California 2004
## 33: San Luis Obispo  7.720455 30.78409 California 2004
## 34:       San Mateo 10.825989 41.09605 California 2004
## 35:   Santa Barbara  6.868000 27.93333 California 2004
## 36:     Santa Clara 11.715455 42.81364 California 2004
## 37:      Santa Cruz  6.760714 27.75000 California 2004
## 38:          Shasta  5.261326 20.00552 California 2004
## 39:        Siskiyou  2.625641 10.95726 California 2004
## 40:          Solano 12.475900 45.71745 California 2004
## 41:          Sonoma  9.096739 34.80435 California 2004
## 42:      Stanislaus 13.770492 48.17486 California 2004
## 43:          Sutter 11.699676 42.90291 California 2004
## 44:         Trinity  2.861739 11.79130 California 2004
## 45:          Tulare 16.644179 56.71930 California 2004
## 46:         Ventura 11.197069 43.08103 California 2004
## 47:            Yolo  9.662947 36.19579 California 2004
##              COUNTY     PM2.5      AQI      STATE year
```

```r
unique(county_2019, by = "COUNTY")
```

```
##              COUNTY     PM2.5      AQI      STATE year
##  1:         Alameda  7.336721 29.82389 California 2019
##  2:           Butte  6.994160 27.66480 California 2019
##  3:       Calaveras  5.460947 22.63314 California 2019
##  4:          Colusa  6.608104 26.77885 California 2019
##  5:    Contra Costa  7.196539 29.40049 California 2019
##  6:       Del Norte  4.934951 20.35599 California 2019
##  7:       El Dorado  2.748023 11.37288 California 2019
##  8:          Fresno  8.530856 32.83108 California 2019
##  9:           Glenn  6.561236 26.77809 California 2019
## 10:        Humboldt  6.787850 27.74766 California 2019
## 11:        Imperial  9.570179 37.55467 California 2019
## 12:            Inyo  4.710421 18.65965 California 2019
## 13:            Kern  8.370988 32.17446 California 2019
## 14:           Kings 12.134410 44.29441 California 2019
## 15:            Lake  3.141667 13.13333 California 2019
## 16:     Los Angeles 10.175245 39.77926 California 2019
## 17:          Madera  9.612885 37.50700 California 2019
## 18:           Marin  5.984683 24.75711 California 2019
## 19:        Mariposa  7.834888 28.65858 California 2019
## 20:       Mendocino  5.702546 23.46535 California 2019
## 21:          Merced  9.274113 36.11065 California 2019
## 22:            Mono  5.442697 21.17191 California 2019
## 23:        Monterey  4.527411 18.77321 California 2019
## 24:            Napa  5.923099 24.45634 California 2019
## 25:          Nevada  5.821673 24.10266 California 2019
## 26:          Orange  8.926352 35.77906 California 2019
## 27:          Placer  6.149640 25.29431 California 2019
## 28:          Plumas  9.277547 34.38113 California 2019
## 29:       Riverside  8.471445 33.51274 California 2019
## 30:      Sacramento  7.117473 27.93988 California 2019
## 31:      San Benito  4.530258 18.86481 California 2019
## 32:  San Bernardino  9.583199 37.23222 California 2019
## 33:       San Diego  9.338319 36.71435 California 2019
## 34:   San Francisco  7.667409 31.28412 California 2019
## 35:     San Joaquin  8.265926 31.89357 California 2019
## 36: San Luis Obispo  5.694247 23.33665 California 2019
## 37:       San Mateo  7.008455 28.66181 California 2019
## 38:   Santa Barbara  5.206791 21.55593 California 2019
## 39:     Santa Clara  7.482000 30.21417 California 2019
## 40:      Santa Cruz  5.620086 23.35725 California 2019
## 41:          Shasta  3.748630 15.09589 California 2019
## 42:        Siskiyou  5.055022 19.65939 California 2019
## 43:          Solano  8.714944 35.19134 California 2019
## 44:          Sonoma  5.678134 23.45190 California 2019
## 45:      Stanislaus  9.140100 34.38221 California 2019
## 46:          Sutter  8.266384 32.40678 California 2019
## 47:          Tehama  5.501719 22.64470 California 2019
## 48:         Trinity  4.944315 19.67055 California 2019
## 49:          Tulare 11.190974 42.15179 California 2019
## 50:         Ventura  6.673925 27.50118 California 2019
## 51:            Yolo  6.849136 27.32593 California 2019
##              COUNTY     PM2.5      AQI      STATE year
```
This line plot shows the average PM2.5 concentration by County in 2004 and 2019. Most of the counties' average PM2.5 concentrations have decreased, as seen by the negative slope.

```r
ggplot(county_combined) +
  geom_point(mapping=aes(x=year, y = PM2.5, group=COUNTY, color=COUNTY)) +
  geom_line(mapping=aes(x=year, y = PM2.5, group=COUNTY, color=COUNTY)) +
  labs(title = "Mean PM2.5 Concentrations per County", x  = "Year", y = "Average PM2.5 Concentration")
```

![](README_files/figure-html/line plot - county-1.png)<!-- -->
Here is a bar graph of the average PM2.5 concentrations per county. The navy bars are the 2004 values and the light blue bars are the 2019 values. There are some counties only containing data for 2019, but the same relationship as the above line plot can be visualized where the average PM2.5 concentration decreases from 2004 to 2019 for most counties.

```r
ggplot(county_combined, mapping=aes(x=COUNTY, y = PM2.5, group = year)) +
  geom_bar(mapping=aes(fill=year),stat='identity', position='dodge') +
  labs(title = "Mean PM2.5 Concentrations per County", y = "Average PM2.5 Concentration") +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))
```

![](README_files/figure-html/barplot-county-1.png)<!-- -->
### Sites in Los Angeles 

```r
##Subset
LA_2004 <- data2004_v2[COUNTY == "Los Angeles"]
LA_2019 <- data2019_v2[COUNTY == "Los Angeles"]
##Calculate average PM2.5 and AQI by site name
LA_2004_avg <- LA_2004[, .(
  PM2.5     = mean(`Daily Mean PM2.5 Concentration`, na.rm=TRUE),
  AQI       = mean(DAILY_AQI_VALUE, na.rm=TRUE),`Site ID`), by = "Site Name"]
LA_2019_avg <- LA_2019[, .(
  PM2.5     = mean(`Daily Mean PM2.5 Concentration`, na.rm=TRUE),
  AQI       = mean(DAILY_AQI_VALUE, na.rm=TRUE),`Site ID`), by = "Site Name"]
##Combine the datasets
LA_2004_avg[, year := 2004]
LA_2019_avg[, year := 2019]
LA_combined <- rbind(LA_2004_avg, LA_2019_avg)
```
Here we can see the average PM2.5 concentrations and AQI values per site in LA for each year

```r
unique(LA_2004_avg, by = "Site Name")
```

```
##                         Site Name     PM2.5      AQI  Site ID year
##  1:                         Azusa 18.405376 61.90323 60370002 2004
##  2:                       Burbank 19.231193 64.87156 60371002 2004
##  3: Los Angeles-North Main Street 20.050841 66.65607 60371103 2004
##  4:                        Reseda 15.574528 55.64151 60371201 2004
##  5:                       Lynwood 18.540870 63.17391 60371301 2004
##  6:                               19.945370 66.84259 60371601 2004
##  7:                      Pasadena 16.631858 58.52212 60372005 2004
##  8:            Long Beach (North) 17.634462 60.97538 60374002 2004
##  9:            Long Beach (South) 16.603670 58.47401 60374004 2004
## 10:     Lancaster-Division Street  8.504505 34.95495 60379033 2004
## 11:                         Lebec  4.138261 17.28696 60379034 2004
```

```r
unique(LA_2019_avg, by = "Site Name")
```

```
##                          Site Name     PM2.5      AQI  Site ID year
##  1:                          Azusa  9.686777 37.57851 60370002 2019
##  2:                       Glendora 11.882222 45.27222 60370016 2019
##  3:  Los Angeles-North Main Street 11.606813 44.86028 60371103 2019
##  4:                         Reseda 11.206875 43.31458 60371201 2019
##  5:                        Compton 11.026073 43.12541 60371302 2019
##  6:                 Pico Rivera #2 10.387079 41.00562 60371602 2019
##  7:                       Pasadena  8.990286 35.66286 60372005 2019
##  8:             Long Beach (North)  9.018239 36.23270 60374002 2019
##  9:             Long Beach (South)  9.940642 39.38268 60374004 2019
## 10: Long Beach-Route 710 Near Road 12.105626 46.55556 60374008 2019
## 11:                  Santa Clarita  6.698324 27.13687 60376012 2019
## 12:      Lancaster-Division Street  6.187955 25.79272 60379033 2019
## 13:                          Lebec  3.148077 13.13462 60379034 2019
```
Here is a line plot showing the average PM2.5 Concentrations per site in Los Angeles for 2004 and 2019. Of the sites for which there is data from both years, the average PM2.5 concentration has decreased. The Lebec and Lancaster-Division Street sites have the smallest amount of change in average PM2.5 concentration.

```r
ggplot(LA_combined) +
  geom_point(mapping=aes(x=year, y = PM2.5, group=`Site Name`, color=`Site Name`)) +
  geom_line(mapping=aes(x=year, y = PM2.5, group=`Site Name`, color=`Site Name`)) +
  labs(title = "LA County-wide PM2.5 Concentrations", x  = "Year", y = "Average PM2.5 Concentration")
```

![](README_files/figure-html/LA lineplot-1.png)<!-- -->
