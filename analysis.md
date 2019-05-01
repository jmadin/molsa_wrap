Analysis
================
Me
5/1/2019

## Todo

  - Setup Git
  - Use Rmarkdown
  - Push to GitHub
  - Use tidyverse
  - Organise a project
  - Do some
work.

## Which way do they want to do it?

## Data

``` r
  data <- read_csv("https://raw.githubusercontent.com/jmadin/himbr/master/data/seed_root_herbivores.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Plot = col_character(),
    ##   `Seed herbivore` = col_logical(),
    ##   `Root herbivore` = col_logical(),
    ##   `No stems` = col_double(),
    ##   Height = col_double(),
    ##   Weight = col_double(),
    ##   `Seed heads` = col_double(),
    ##   `Seeds in 25 heads` = col_double()
    ## )

``` r
  data
```

    ## # A tibble: 169 x 8
    ##    Plot  `Seed herbivore` `Root herbivore` `No stems` Height Weight
    ##    <chr> <lgl>            <lgl>                 <dbl>  <dbl>  <dbl>
    ##  1 plot… TRUE             TRUE                      1     31   4.16
    ##  2 plot… TRUE             TRUE                      3     41   5.82
    ##  3 plot… TRUE             TRUE                      1     42   3.51
    ##  4 plot… TRUE             FALSE                     1     64   7.16
    ##  5 plot… TRUE             FALSE                     1     47   6.17
    ##  6 plot… TRUE             FALSE                     1     52   5.32
    ##  7 plot… FALSE            TRUE                      3     57  23.4 
    ##  8 plot… TRUE             TRUE                      2     27   1.76
    ##  9 plot… TRUE             TRUE                      1     40   4.01
    ## 10 plot… TRUE             TRUE                      1     33   2.58
    ## # ... with 159 more rows, and 2 more variables: `Seed heads` <dbl>, `Seeds
    ## #   in 25 heads` <dbl>

``` r
  data %>%
  select(Height, Weight)
```

    ## # A tibble: 169 x 2
    ##    Height Weight
    ##     <dbl>  <dbl>
    ##  1     31   4.16
    ##  2     41   5.82
    ##  3     42   3.51
    ##  4     64   7.16
    ##  5     47   6.17
    ##  6     52   5.32
    ##  7     57  23.4 
    ##  8     27   1.76
    ##  9     40   4.01
    ## 10     33   2.58
    ## # ... with 159 more rows

``` r
  plot(Weight ~ Height, data)
```

![](analysis_files/figure-gfm/analysis-1.png)<!-- -->

``` r
  data %>%
  select(Height, Weight)
```

    ## # A tibble: 169 x 2
    ##    Height Weight
    ##     <dbl>  <dbl>
    ##  1     31   4.16
    ##  2     41   5.82
    ##  3     42   3.51
    ##  4     64   7.16
    ##  5     47   6.17
    ##  6     52   5.32
    ##  7     57  23.4 
    ##  8     27   1.76
    ##  9     40   4.01
    ## 10     33   2.58
    ## # ... with 159 more rows

``` r
  data <- data %>%
    mutate(Height_log10 = log10(Height), Weight_log10 = log10(Weight))
  
  pdf("output/figure1.pdf")  
    plot(Weight_log10 ~ Height_log10, data)
  
    mod <- lm(Weight_log10 ~ Height_log10, data)
    x <- sort(data$Height_log10)
    pred <- predict(mod, list(Height_log10=x), interval="prediction")
  
    lines(x, pred[,1])
    polygon(c(x, rev(x)), c(pred[,2], rev(pred[,3])), col=rgb(0, 0, 0, 0.2), border=NA)
    dev.off()
```

    ## quartz_off_screen 
    ##                 2

-----

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax
for authoring HTML, PDF, and MS Word documents. For more details on
using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

``` r
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

## Including Plots

You can also embed plots, for example:

![](analysis_files/figure-gfm/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.
