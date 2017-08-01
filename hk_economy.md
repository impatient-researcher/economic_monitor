Hong Kong Economy
================
2017/08/01

-   [Aim](#aim)
-   [Real GDP](#real-gdp)
-   [References](#references)

Aim
---

-   understand key statistics of hong kong's economy in the past 20 years.
-   a showcase of beautiful charts

Real GDP
--------

``` r
gdp_cat <- WDIsearch("gdp")

gdp_growth <- WDI(indicator="NY.GDP.MKTP.KD.ZG", country = c("HK", "CN", "US"),
                  start=1980, end=2017)

gdp_growth_sum_st <- gdp_growth %>%
  group_by(country) %>%
  summarise(mean_growth = round(mean(NY.GDP.MKTP.KD.ZG),2),
            sd_growth =  round(sd(NY.GDP.MKTP.KD.ZG),2))

gdp_growth_sum_st
```

    ## # A tibble: 3 x 3
    ##                country mean_growth sd_growth
    ##                  <chr>       <dbl>     <dbl>
    ## 1                China        9.66      2.72
    ## 2 Hong Kong SAR, China        4.77      3.82
    ## 3        United States        2.61      1.93

``` r
gdp_growth_plot <- gdp_growth %>%
  filter(year >= 2000) %>%
  ggplot(.,aes(x = year, y = NY.GDP.MKTP.KD.ZG, group = country)) + geom_line(aes(colour = country)) + theme_fivethirtyeight() +
  labs(title = "Real GDP Growth - 2000 to 2016", subtitle = "Annual % Growth")

gdp_growth_plot
```

![](hk_economy_files/figure-markdown_github-ascii_identifiers/unnamed-chunk-1-1.png)

References
----------

-   [how to use WDI package in R](https://cran.r-project.org/web/packages/WDI/README.html)
