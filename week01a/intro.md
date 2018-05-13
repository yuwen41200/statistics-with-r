Hello World
================
no\_name
2018-02-27

``` r
Sys.setlocale(category = "LC_ALL", locale = "cht")
```

    ## Warning in Sys.setlocale(category = "LC_ALL", locale = "cht"): 作業系統回報
    ## 無法實現設定語區為 "cht" 的要求

    ## [1] ""

``` r
foo <- c("中文", "測試", "可以", "輸出")
foo
```

    ## [1] "中文" "測試" "可以" "輸出"

``` r
foo <- foo[foo != "中文"]
foo
```

    ## [1] "測試" "可以" "輸出"

``` r
foo <- c(foo, "新增")
foo
```

    ## [1] "測試" "可以" "輸出" "新增"

``` r
bar <- c(10, 20, 30, 40)
bar
```

    ## [1] 10 20 30 40

``` r
foobar <- data.frame(name = foo, age = bar)
foobar
```

    ##   name age
    ## 1 測試  10
    ## 2 可以  20
    ## 3 輸出  30
    ## 4 新增  40

``` r
foobar$other <- c("a", "b", "c", "d")
foobar
```

    ##   name age other
    ## 1 測試  10     a
    ## 2 可以  20     b
    ## 3 輸出  30     c
    ## 4 新增  40     d

![](intro_files/figure-markdown_github/pressure-1.png)
