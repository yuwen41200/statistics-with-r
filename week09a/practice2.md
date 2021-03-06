Week 9 Practice 2
================
Yu-Wen Pu
2018-04-24

``` r
knitr::opts_chunk$set(results = "hold", fig.retina = 2)
set.seed(1830)
```

資料處理
--------

``` r
survey <- read.table("../week7/2018class.csv", header = TRUE, sep = ",")
str(survey)
```

    ## 'data.frame':    34 obs. of  10 variables:
    ##  $ height   : int  153 162 158 176 181 181 161 165 151 176 ...
    ##  $ heartbeat: int  72 69 66 78 72 70 80 70 76 80 ...
    ##  $ gender   : int  1 1 1 2 2 2 1 1 1 2 ...
    ##  $ haircut  : int  0 650 600 200 200 100 650 1200 560 160 ...
    ##  $ lunch    : int  65 70 65 70 75 70 88 110 65 80 ...
    ##  $ money    : int  1200 455 276 4000 735 200 2500 2845 178 9811 ...
    ##  $ random   : int  8888 1000 5542 1111 5487 8591 1024 5678 1000 5649 ...
    ##  $ smoke    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ sleep    : int  0 0 0 23 23 0 0 0 0 0 ...
    ##  $ profage  : int  50 53 55 45 59 52 52 47 42 19 ...

``` r
survey$tot_money <- survey$haircut + survey$lunch
str(survey)
```

    ## 'data.frame':    34 obs. of  11 variables:
    ##  $ height   : int  153 162 158 176 181 181 161 165 151 176 ...
    ##  $ heartbeat: int  72 69 66 78 72 70 80 70 76 80 ...
    ##  $ gender   : int  1 1 1 2 2 2 1 1 1 2 ...
    ##  $ haircut  : int  0 650 600 200 200 100 650 1200 560 160 ...
    ##  $ lunch    : int  65 70 65 70 75 70 88 110 65 80 ...
    ##  $ money    : int  1200 455 276 4000 735 200 2500 2845 178 9811 ...
    ##  $ random   : int  8888 1000 5542 1111 5487 8591 1024 5678 1000 5649 ...
    ##  $ smoke    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ sleep    : int  0 0 0 23 23 0 0 0 0 0 ...
    ##  $ profage  : int  50 53 55 45 59 52 52 47 42 19 ...
    ##  $ tot_money: int  65 720 665 270 275 170 738 1310 625 240 ...

``` r
survey$hb_level[survey$heartbeat >= 80] <- "high"
survey$hb_level[survey$heartbeat < 80 & survey$heartbeat > 70] <- "mid"
survey$hb_level[survey$heartbeat <= 70] <- "low"
str(survey)
```

    ## 'data.frame':    34 obs. of  12 variables:
    ##  $ height   : int  153 162 158 176 181 181 161 165 151 176 ...
    ##  $ heartbeat: int  72 69 66 78 72 70 80 70 76 80 ...
    ##  $ gender   : int  1 1 1 2 2 2 1 1 1 2 ...
    ##  $ haircut  : int  0 650 600 200 200 100 650 1200 560 160 ...
    ##  $ lunch    : int  65 70 65 70 75 70 88 110 65 80 ...
    ##  $ money    : int  1200 455 276 4000 735 200 2500 2845 178 9811 ...
    ##  $ random   : int  8888 1000 5542 1111 5487 8591 1024 5678 1000 5649 ...
    ##  $ smoke    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ sleep    : int  0 0 0 23 23 0 0 0 0 0 ...
    ##  $ profage  : int  50 53 55 45 59 52 52 47 42 19 ...
    ##  $ tot_money: int  65 720 665 270 275 170 738 1310 625 240 ...
    ##  $ hb_level : chr  "mid" "low" "low" "mid" ...

``` r
names(survey)[10] <- "prof_age"  # set the names of an object
str(survey)
```

    ## 'data.frame':    34 obs. of  12 variables:
    ##  $ height   : int  153 162 158 176 181 181 161 165 151 176 ...
    ##  $ heartbeat: int  72 69 66 78 72 70 80 70 76 80 ...
    ##  $ gender   : int  1 1 1 2 2 2 1 1 1 2 ...
    ##  $ haircut  : int  0 650 600 200 200 100 650 1200 560 160 ...
    ##  $ lunch    : int  65 70 65 70 75 70 88 110 65 80 ...
    ##  $ money    : int  1200 455 276 4000 735 200 2500 2845 178 9811 ...
    ##  $ random   : int  8888 1000 5542 1111 5487 8591 1024 5678 1000 5649 ...
    ##  $ smoke    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ sleep    : int  0 0 0 23 23 0 0 0 0 0 ...
    ##  $ prof_age : int  50 53 55 45 59 52 52 47 42 19 ...
    ##  $ tot_money: int  65 720 665 270 275 170 738 1310 625 240 ...
    ##  $ hb_level : chr  "mid" "low" "low" "mid" ...

``` r
survey[, 1:3]
survey[5:10, ]
survey[order(survey$height), ]
```

    ##    height heartbeat gender
    ## 1     153        72      1
    ## 2     162        69      1
    ## 3     158        66      1
    ## 4     176        78      2
    ## 5     181        72      2
    ## 6     181        70      2
    ## 7     161        80      1
    ## 8     165        70      1
    ## 9     151        76      1
    ## 10    176        80      2
    ## 11    175        75      2
    ## 12    173        80      2
    ## 13    177        70      2
    ## 14    157        84      1
    ## 15    158        70      1
    ## 16    158        84      1
    ## 17    168        80      1
    ## 18    165        64      1
    ## 19    168        71      1
    ## 20    163        69      1
    ## 21    163        72      1
    ## 22    159        80      1
    ## 23    163        56      1
    ## 24    163        78      1
    ## 25    160        74      1
    ## 26    160        90      1
    ## 27    174        66      2
    ## 28    160        90      1
    ## 29    153        78      1
    ## 30    157        70      1
    ## 31    167        78      1
    ## 32    176        66      2
    ## 33    176        92      2
    ## 34    165        67      1
    ##    height heartbeat gender haircut lunch money random smoke sleep prof_age
    ## 5     181        72      2     200    75   735   5487     1    23       59
    ## 6     181        70      2     100    70   200   8591     1     0       52
    ## 7     161        80      1     650    88  2500   1024     1     0       52
    ## 8     165        70      1    1200   110  2845   5678     1     0       47
    ## 9     151        76      1     560    65   178   1000     1     0       42
    ## 10    176        80      2     160    80  9811   5649     1     0       19
    ##    tot_money hb_level
    ## 5        275      mid
    ## 6        170      low
    ## 7        738     high
    ## 8       1310      low
    ## 9        625      mid
    ## 10       240     high
    ##    height heartbeat gender haircut lunch money random smoke sleep prof_age
    ## 9     151        76      1     560    65   178   1000     1     0       42
    ## 1     153        72      1       0    65  1200   8888     1     0       50
    ## 29    153        78      1     500    80   500   1993     1     1       55
    ## 14    157        84      1     500    30    57   1787     1     3       57
    ## 30    157        70      1     169   107   480   1111     1     1       55
    ## 3     158        66      1     600    65   276   5542     1     0       55
    ## 15    158        70      1     500    65   900   8888     1     3       50
    ## 16    158        84      1    5400    65 50000   7777     1     3       45
    ## 22    159        80      1    3000   103   700   5649     1     2       45
    ## 25    160        74      1     300   125  1535   4444     1     2       60
    ## 26    160        90      1     500    60  3000   1009     1     1       43
    ## 28    160        90      1     500    60  1000   1455     1     1       50
    ## 7     161        80      1     650    88  2500   1024     1     0       52
    ## 2     162        69      1     650    70   455   1000     1     0       53
    ## 20    163        69      1     150   103  2752   1333     1     3       48
    ## 21    163        72      1     100   600 10000   5000     1     3       40
    ## 23    163        56      1    2500   103  1064   9487     2     2       55
    ## 24    163        78      1     650    85   750   7863     1     2       48
    ## 8     165        70      1    1200   110  2845   5678     1     0       47
    ## 18    165        64      1     120    40  1003   1568     1     3       45
    ## 34    165        67      1     800    22   127   9998     1     1       35
    ## 31    167        78      1     500     0   513   1576     1     1       47
    ## 17    168        80      1     400   103   567   6666     1     3       50
    ## 19    168        71      1      50    49  1000   9998     1     3       46
    ## 12    173        80      2     400    22   100   2654     1     4       35
    ## 27    174        66      2     100   110  1500   4999     1     1       52
    ## 11    175        75      2     100    90  2800   1001     1     0       43
    ## 4     176        78      2     200    70  4000   1111     1    23       45
    ## 10    176        80      2     160    80  9811   5649     1     0       19
    ## 32    176        66      2     150   119  1500   1111     1     1       50
    ## 33    176        92      2     100    75  6268   3142     1     1       33
    ## 13    177        70      2      50    85  5000   1319     1     3       48
    ## 5     181        72      2     200    75   735   5487     1    23       59
    ## 6     181        70      2     100    70   200   8591     1     0       52
    ##    tot_money hb_level
    ## 9        625      mid
    ## 1         65      mid
    ## 29       580      mid
    ## 14       530     high
    ## 30       276      low
    ## 3        665      low
    ## 15       565      low
    ## 16      5465     high
    ## 22      3103     high
    ## 25       425      mid
    ## 26       560     high
    ## 28       560     high
    ## 7        738     high
    ## 2        720      low
    ## 20       253      low
    ## 21       700      mid
    ## 23      2603      low
    ## 24       735      mid
    ## 8       1310      low
    ## 18       160      low
    ## 34       822      low
    ## 31       500      mid
    ## 17       503     high
    ## 19        99      mid
    ## 12       422     high
    ## 27       210      low
    ## 11       190      mid
    ## 4        270      mid
    ## 10       240     high
    ## 32       269      low
    ## 33       175     high
    ## 13       135      low
    ## 5        275      mid
    ## 6        170      low

``` r
subset(survey, heartbeat >= 75 & gender == "1", select = haircut:hb_level)
```

    ##    haircut lunch money random smoke sleep prof_age tot_money hb_level
    ## 7      650    88  2500   1024     1     0       52       738     high
    ## 9      560    65   178   1000     1     0       42       625      mid
    ## 14     500    30    57   1787     1     3       57       530     high
    ## 16    5400    65 50000   7777     1     3       45      5465     high
    ## 17     400   103   567   6666     1     3       50       503     high
    ## 22    3000   103   700   5649     1     2       45      3103     high
    ## 24     650    85   750   7863     1     2       48       735      mid
    ## 26     500    60  3000   1009     1     1       43       560     high
    ## 28     500    60  1000   1455     1     1       50       560     high
    ## 29     500    80   500   1993     1     1       55       580      mid
    ## 31     500     0   513   1576     1     1       47       500      mid

``` r
# 隨機抽樣，取後不放回
survey[sample(1:nrow(survey), 5, replace = FALSE), ]
```

    ##    height heartbeat gender haircut lunch money random smoke sleep prof_age
    ## 4     176        78      2     200    70  4000   1111     1    23       45
    ## 14    157        84      1     500    30    57   1787     1     3       57
    ## 3     158        66      1     600    65   276   5542     1     0       55
    ## 27    174        66      2     100   110  1500   4999     1     1       52
    ## 25    160        74      1     300   125  1535   4444     1     2       60
    ##    tot_money hb_level
    ## 4        270      mid
    ## 14       530     high
    ## 3        665      low
    ## 27       210      low
    ## 25       425      mid
