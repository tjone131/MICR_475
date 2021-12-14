homework 5\_plots for flights
================
Theresa Jones
9/17/2021

``` r
library(tidyverse)
library(dplyr)
glimpse(diamonds)
```

    ## Rows: 53,940
    ## Columns: 10
    ## $ carat   <dbl> 0.23, 0.21, 0.23, 0.29, 0.31, 0.24, 0.24, 0.26, 0.22, 0.23, 0.…
    ## $ cut     <ord> Ideal, Premium, Good, Premium, Good, Very Good, Very Good, Ver…
    ## $ color   <ord> E, E, E, I, J, J, I, H, E, H, J, J, F, J, E, E, I, J, J, J, I,…
    ## $ clarity <ord> SI2, SI1, VS1, VS2, SI2, VVS2, VVS1, SI1, VS2, VS1, SI1, VS1, …
    ## $ depth   <dbl> 61.5, 59.8, 56.9, 62.4, 63.3, 62.8, 62.3, 61.9, 65.1, 59.4, 64…
    ## $ table   <dbl> 55, 61, 65, 58, 58, 57, 57, 55, 61, 61, 55, 56, 61, 54, 62, 58…
    ## $ price   <int> 326, 326, 327, 334, 335, 336, 336, 337, 337, 338, 339, 340, 34…
    ## $ x       <dbl> 3.95, 3.89, 4.05, 4.20, 4.34, 3.94, 3.95, 4.07, 3.87, 4.00, 4.…
    ## $ y       <dbl> 3.98, 3.84, 4.07, 4.23, 4.35, 3.96, 3.98, 4.11, 3.78, 4.05, 4.…
    ## $ z       <dbl> 2.43, 2.31, 2.31, 2.63, 2.75, 2.48, 2.47, 2.53, 2.49, 2.39, 2.…

``` r
diamonds %>% count(cut)
```

    ## # A tibble: 5 × 2
    ##   cut           n
    ##   <ord>     <int>
    ## 1 Fair       1610
    ## 2 Good       4906
    ## 3 Very Good 12082
    ## 4 Premium   13791
    ## 5 Ideal     21551

``` r
cuts.of.diamonds <- diamonds %>% count(cut)
```

``` r
sample_frac(diamonds,.01,replace=TRUE)
```

    ## # A tibble: 539 × 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  0.67 Good      F     VS1      59.8  60.3  2479  5.62  5.69  3.38
    ##  2  0.51 Very Good F     VS1      62.4  59    1697  5.04  5.09  3.16
    ##  3  1.06 Ideal     F     SI1      61.3  57    4862  6.56  6.51  4.01
    ##  4  0.3  Premium   G     VVS2     61    60     878  4.32  4.3   2.63
    ##  5  0.35 Ideal     D     SI1      61.6  56     644  4.49  4.53  2.78
    ##  6  1.14 Ideal     D     VS1      59.8  57    9193  6.83  6.74  4.06
    ##  7  0.33 Very Good G     VVS2     63    57     752  4.38  4.42  2.77
    ##  8  0.41 Ideal     G     SI1      62.9  56     923  4.75  4.7   2.97
    ##  9  0.32 Very Good G     VS1      61.2  62     602  4.41  4.45  2.71
    ## 10  1.01 Premium   H     VS2      62.6  60    4745  6.39  6.36  3.99
    ## # … with 529 more rows

``` r
 clarity_carat <- diamonds %>%
  group_by(clarity) %>%
  slice_max(carat, n=100) %>%
  summarise(average.size = mean (carat, na.rm = TRUE))
print(clarity_carat)
```

    ## # A tibble: 8 × 2
    ##   clarity average.size
    ##   <ord>          <dbl>
    ## 1 I1              2.46
    ## 2 SI2             2.62
    ## 3 SI1             2.29
    ## 4 VS2             2.22
    ## 5 VS1             2.10
    ## 6 VVS2            1.64
    ## 7 VVS1            1.50
    ## 8 IF              1.39

``` r
ggplot(data = diamonds) +
   geom_point(mapping = aes(x = x, y = y, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#4-1.png)<!-- -->

``` r
ggplot(data = diamonds) +
   geom_point(mapping = aes(x = x, y = z, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#4-2.png)<!-- -->

``` r
diamonds2 <- filter(diamonds, x > 3 & z < 10 & y < 20 & z > 2)
ggplot(data = diamonds2) +
   geom_point(mapping = aes(x = x, y = y, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#5-1.png)<!-- -->

``` r
ggplot(data = diamonds2) +
   geom_point(mapping = aes(x = x, y = z, color = clarity))
```

![](homework_5--working-with-diamonds-and-dplyr_files/figure-gfm/question%20#5-2.png)<!-- -->
