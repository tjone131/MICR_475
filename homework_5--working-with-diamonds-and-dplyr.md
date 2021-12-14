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
    ##  1  1.02 Ideal     F     VS1      62      57  8637  6.49  6.44  4.01
    ##  2  0.3  Very Good F     SI1      62.1    60   500  4.26  4.28  2.65
    ##  3  0.71 Ideal     H     SI1      62.1    57  2313  5.68  5.73  3.54
    ##  4  0.76 Ideal     F     SI2      61.1    55  2469  5.9   5.94  3.62
    ##  5  0.31 Ideal     G     IF       61.3    56   891  4.38  4.4   2.69
    ##  6  0.5  Ideal     F     VVS1     61      57  2165  5.13  5.16  3.14
    ##  7  0.3  Premium   H     VS2      62.2    59   608  4.31  4.28  2.67
    ##  8  0.7  Very Good G     VVS2     62.9    59  2848  5.61  5.68  3.55
    ##  9  0.35 Very Good G     IF       62.6    59   898  4.43  4.49  2.79
    ## 10  0.46 Fair      G     VS1      58      66  1035  5.08  5.03  2.93
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
