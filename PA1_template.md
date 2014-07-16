# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
Assessment data will be loaded directly from zip file:

```r
assessment.data <- read.csv(unzip("activity.zip", "activity.csv"))
```
Lets examine structure of crated data frame:

```r
str(assessment.data)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```
We can see that data type for **date** is *Factor*, and it probably should be *Date*. Let's adjust that:

```r
assessment.data$date <- as.Date(assessment.data$date)
```
Simple summary of readed data:

```r
summary(assessment.data)
```

```
##      steps            date               interval   
##  Min.   :  0.0   Min.   :2012-10-01   Min.   :   0  
##  1st Qu.:  0.0   1st Qu.:2012-10-16   1st Qu.: 589  
##  Median :  0.0   Median :2012-10-31   Median :1178  
##  Mean   : 37.4   Mean   :2012-10-31   Mean   :1178  
##  3rd Qu.: 12.0   3rd Qu.:2012-11-15   3rd Qu.:1766  
##  Max.   :806.0   Max.   :2012-11-30   Max.   :2355  
##  NA's   :2304
```
## What is mean total number of steps taken per day?
Sum of steps for each day. Steps variable is **x**:

```r
total.steps.day <- aggregate.data.frame(x = assessment.data$steps, by = list(Date = assessment.data$date), sum)
total.steps.day
```

```
##          Date     x
## 1  2012-10-01    NA
## 2  2012-10-02   126
## 3  2012-10-03 11352
## 4  2012-10-04 12116
## 5  2012-10-05 13294
## 6  2012-10-06 15420
## 7  2012-10-07 11015
## 8  2012-10-08    NA
## 9  2012-10-09 12811
## 10 2012-10-10  9900
## 11 2012-10-11 10304
## 12 2012-10-12 17382
## 13 2012-10-13 12426
## 14 2012-10-14 15098
## 15 2012-10-15 10139
## 16 2012-10-16 15084
## 17 2012-10-17 13452
## 18 2012-10-18 10056
## 19 2012-10-19 11829
## 20 2012-10-20 10395
## 21 2012-10-21  8821
## 22 2012-10-22 13460
## 23 2012-10-23  8918
## 24 2012-10-24  8355
## 25 2012-10-25  2492
## 26 2012-10-26  6778
## 27 2012-10-27 10119
## 28 2012-10-28 11458
## 29 2012-10-29  5018
## 30 2012-10-30  9819
## 31 2012-10-31 15414
## 32 2012-11-01    NA
## 33 2012-11-02 10600
## 34 2012-11-03 10571
## 35 2012-11-04    NA
## 36 2012-11-05 10439
## 37 2012-11-06  8334
## 38 2012-11-07 12883
## 39 2012-11-08  3219
## 40 2012-11-09    NA
## 41 2012-11-10    NA
## 42 2012-11-11 12608
## 43 2012-11-12 10765
## 44 2012-11-13  7336
## 45 2012-11-14    NA
## 46 2012-11-15    41
## 47 2012-11-16  5441
## 48 2012-11-17 14339
## 49 2012-11-18 15110
## 50 2012-11-19  8841
## 51 2012-11-20  4472
## 52 2012-11-21 12787
## 53 2012-11-22 20427
## 54 2012-11-23 21194
## 55 2012-11-24 14478
## 56 2012-11-25 11834
## 57 2012-11-26 11162
## 58 2012-11-27 13646
## 59 2012-11-28 10183
## 60 2012-11-29  7047
## 61 2012-11-30    NA
```
Histogram:

```r
hist(total.steps.day$x)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

Mean and median values:

```r
mean.steps <- mean(total.steps.day$x, na.rm = T)
median.steps <- median(total.steps.day$x, na.rm = T)
mean.steps
```

```
## [1] 10766
```

```r
median.steps
```

```
## [1] 10765
```

## What is the average daily activity pattern?
Lets load plotting library:

```r
library("ggplot2")
```
Sum of steps for each interval. Steps variable is **x**:

```r
total.steps.interval <- aggregate.data.frame(x = assessment.data$steps, by = list(Interval = assessment.data$interval), sum)
total.steps.interval
```

```
##     Interval  x
## 1          0 NA
## 2          5 NA
## 3         10 NA
## 4         15 NA
## 5         20 NA
## 6         25 NA
## 7         30 NA
## 8         35 NA
## 9         40 NA
## 10        45 NA
## 11        50 NA
## 12        55 NA
## 13       100 NA
## 14       105 NA
## 15       110 NA
## 16       115 NA
## 17       120 NA
## 18       125 NA
## 19       130 NA
## 20       135 NA
## 21       140 NA
## 22       145 NA
## 23       150 NA
## 24       155 NA
## 25       200 NA
## 26       205 NA
## 27       210 NA
## 28       215 NA
## 29       220 NA
## 30       225 NA
## 31       230 NA
## 32       235 NA
## 33       240 NA
## 34       245 NA
## 35       250 NA
## 36       255 NA
## 37       300 NA
## 38       305 NA
## 39       310 NA
## 40       315 NA
## 41       320 NA
## 42       325 NA
## 43       330 NA
## 44       335 NA
## 45       340 NA
## 46       345 NA
## 47       350 NA
## 48       355 NA
## 49       400 NA
## 50       405 NA
## 51       410 NA
## 52       415 NA
## 53       420 NA
## 54       425 NA
## 55       430 NA
## 56       435 NA
## 57       440 NA
## 58       445 NA
## 59       450 NA
## 60       455 NA
## 61       500 NA
## 62       505 NA
## 63       510 NA
## 64       515 NA
## 65       520 NA
## 66       525 NA
## 67       530 NA
## 68       535 NA
## 69       540 NA
## 70       545 NA
## 71       550 NA
## 72       555 NA
## 73       600 NA
## 74       605 NA
## 75       610 NA
## 76       615 NA
## 77       620 NA
## 78       625 NA
## 79       630 NA
## 80       635 NA
## 81       640 NA
## 82       645 NA
## 83       650 NA
## 84       655 NA
## 85       700 NA
## 86       705 NA
## 87       710 NA
## 88       715 NA
## 89       720 NA
## 90       725 NA
## 91       730 NA
## 92       735 NA
## 93       740 NA
## 94       745 NA
## 95       750 NA
## 96       755 NA
## 97       800 NA
## 98       805 NA
## 99       810 NA
## 100      815 NA
## 101      820 NA
## 102      825 NA
## 103      830 NA
## 104      835 NA
## 105      840 NA
## 106      845 NA
## 107      850 NA
## 108      855 NA
## 109      900 NA
## 110      905 NA
## 111      910 NA
## 112      915 NA
## 113      920 NA
## 114      925 NA
## 115      930 NA
## 116      935 NA
## 117      940 NA
## 118      945 NA
## 119      950 NA
## 120      955 NA
## 121     1000 NA
## 122     1005 NA
## 123     1010 NA
## 124     1015 NA
## 125     1020 NA
## 126     1025 NA
## 127     1030 NA
## 128     1035 NA
## 129     1040 NA
## 130     1045 NA
## 131     1050 NA
## 132     1055 NA
## 133     1100 NA
## 134     1105 NA
## 135     1110 NA
## 136     1115 NA
## 137     1120 NA
## 138     1125 NA
## 139     1130 NA
## 140     1135 NA
## 141     1140 NA
## 142     1145 NA
## 143     1150 NA
## 144     1155 NA
## 145     1200 NA
## 146     1205 NA
## 147     1210 NA
## 148     1215 NA
## 149     1220 NA
## 150     1225 NA
## 151     1230 NA
## 152     1235 NA
## 153     1240 NA
## 154     1245 NA
## 155     1250 NA
## 156     1255 NA
## 157     1300 NA
## 158     1305 NA
## 159     1310 NA
## 160     1315 NA
## 161     1320 NA
## 162     1325 NA
## 163     1330 NA
## 164     1335 NA
## 165     1340 NA
## 166     1345 NA
## 167     1350 NA
## 168     1355 NA
## 169     1400 NA
## 170     1405 NA
## 171     1410 NA
## 172     1415 NA
## 173     1420 NA
## 174     1425 NA
## 175     1430 NA
## 176     1435 NA
## 177     1440 NA
## 178     1445 NA
## 179     1450 NA
## 180     1455 NA
## 181     1500 NA
## 182     1505 NA
## 183     1510 NA
## 184     1515 NA
## 185     1520 NA
## 186     1525 NA
## 187     1530 NA
## 188     1535 NA
## 189     1540 NA
## 190     1545 NA
## 191     1550 NA
## 192     1555 NA
## 193     1600 NA
## 194     1605 NA
## 195     1610 NA
## 196     1615 NA
## 197     1620 NA
## 198     1625 NA
## 199     1630 NA
## 200     1635 NA
## 201     1640 NA
## 202     1645 NA
## 203     1650 NA
## 204     1655 NA
## 205     1700 NA
## 206     1705 NA
## 207     1710 NA
## 208     1715 NA
## 209     1720 NA
## 210     1725 NA
## 211     1730 NA
## 212     1735 NA
## 213     1740 NA
## 214     1745 NA
## 215     1750 NA
## 216     1755 NA
## 217     1800 NA
## 218     1805 NA
## 219     1810 NA
## 220     1815 NA
## 221     1820 NA
## 222     1825 NA
## 223     1830 NA
## 224     1835 NA
## 225     1840 NA
## 226     1845 NA
## 227     1850 NA
## 228     1855 NA
## 229     1900 NA
## 230     1905 NA
## 231     1910 NA
## 232     1915 NA
## 233     1920 NA
## 234     1925 NA
## 235     1930 NA
## 236     1935 NA
## 237     1940 NA
## 238     1945 NA
## 239     1950 NA
## 240     1955 NA
## 241     2000 NA
## 242     2005 NA
## 243     2010 NA
## 244     2015 NA
## 245     2020 NA
## 246     2025 NA
## 247     2030 NA
## 248     2035 NA
## 249     2040 NA
## 250     2045 NA
## 251     2050 NA
## 252     2055 NA
## 253     2100 NA
## 254     2105 NA
## 255     2110 NA
## 256     2115 NA
## 257     2120 NA
## 258     2125 NA
## 259     2130 NA
## 260     2135 NA
## 261     2140 NA
## 262     2145 NA
## 263     2150 NA
## 264     2155 NA
## 265     2200 NA
## 266     2205 NA
## 267     2210 NA
## 268     2215 NA
## 269     2220 NA
## 270     2225 NA
## 271     2230 NA
## 272     2235 NA
## 273     2240 NA
## 274     2245 NA
## 275     2250 NA
## 276     2255 NA
## 277     2300 NA
## 278     2305 NA
## 279     2310 NA
## 280     2315 NA
## 281     2320 NA
## 282     2325 NA
## 283     2330 NA
## 284     2335 NA
## 285     2340 NA
## 286     2345 NA
## 287     2350 NA
## 288     2355 NA
```
Plot:

```r
ggplot()
```

```
## Error: No layers in plot
```
## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
