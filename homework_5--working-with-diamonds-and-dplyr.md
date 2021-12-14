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
    ##  1  0.57 Ideal     F     IF       61.8    54  2974  5.33  5.35  3.3 
    ##  2  1.01 Ideal     G     SI2      61.5    57  4299  6.5   6.42  3.97
    ##  3  0.5  Premium   D     VS2      61.4    59  1845  5.15  5.11  3.15
    ##  4  0.65 Ideal     D     VVS1     61.8    57  4022  5.54  5.56  3.43
    ##  5  0.52 Very Good D     VS2      63.4    56  1828  5.16  5.09  3.25
    ##  6  0.82 Premium   H     VS2      62.6    59  2939  5.99  5.93  3.73
    ##  7  1.01 Very Good F     VS2      62.8    59  6416  6.33  6.41  4   
    ##  8  1.21 Ideal     G     SI2      62.9    57  4631  6.78  6.73  4.25
    ##  9  0.53 Very Good F     VS1      61.5    59  1821  5.19  5.22  3.2 
    ## 10  0.9  Very Good I     VVS1     63.4    57  3872  6.09  6.12  3.87
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

![question4_chunk1](https://user-images.githubusercontent.com/89625876/145927981-db2112ab-e327-482c-b75f-80bbc914c85a.png)

``` r
ggplot(data = diamonds) +
   geom_point(mapping = aes(x = x, y = z, color = clarity))
```

![question4_2](https://user-images.githubusercontent.com/89625876/145928005-7f44b97d-c580-4e1d-a87e-b77d26c98db5.png)

``` r
diamonds2 <- filter(diamonds, x > 3 & z < 10 & y < 20 & z > 2)
ggplot(data = diamonds2) +
   geom_point(mapping = aes(x = x, y = y, color = clarity))
```

![question5_chunk1](https://user-images.githubusercontent.com/89625876/145928097-e4307ebb-0b5b-4761-8177-7626baab2440.png)

``` r
ggplot(data = diamonds2) +
   geom_point(mapping = aes(x = x, y = z, color = clarity))
```
  
![question5_chunk2](https://user-images.githubusercontent.com/89625876/145928110-69acec43-de09-4945-be4b-194b9e30c9cc.png)
