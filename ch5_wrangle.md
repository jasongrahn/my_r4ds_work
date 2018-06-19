ch\_5\_\_data\_transformation
================

exploring the basic dataframe

``` r
flights
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

Notes from the book:

The verbs to know:

1.  Pick observations by their values (filter()).
2.  Reorder the rows (arrange()).
3.  Pick variables by their names (select()).
4.  Create new variables with functions of existing variables (mutate()).
5.  Collapse many values down to a single summary (summarise()).

All verbs work similarly:

1.  The first argument is a data frame.
2.  The subsequent arguments describe what to do with the data frame, using the variable names (without quotes).
3.  The result is a new data frame.

Together, the verbs make it easy to chain together multiple simple steps to achieve a complex result.

filter
------

``` r
#filter the flights data for the first month and first day
filter(flights, month == 1, day == 1)
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 832 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

wrapping a command in `()` will run the results AND show the output. Note the difference:

``` r
dec25 <- filter(flights, month == 12, day == 25)

(dec25 <- filter(flights, month == 12, day == 25))
```

    ## # A tibble: 719 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013    12    25      456            500        -4      649
    ##  2  2013    12    25      524            515         9      805
    ##  3  2013    12    25      542            540         2      832
    ##  4  2013    12    25      546            550        -4     1022
    ##  5  2013    12    25      556            600        -4      730
    ##  6  2013    12    25      557            600        -3      743
    ##  7  2013    12    25      557            600        -3      818
    ##  8  2013    12    25      559            600        -1      855
    ##  9  2013    12    25      559            600        -1      849
    ## 10  2013    12    25      600            600         0      850
    ## # ... with 709 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

using `OR` aka `|`

``` r
#this doesn't work to find flights in november OR december
filter(flights, month == 11 | 12)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      542            540         2      923
    ##  4  2013     1     1      544            545        -1     1004
    ##  5  2013     1     1      554            600        -6      812
    ##  6  2013     1     1      554            558        -4      740
    ##  7  2013     1     1      555            600        -5      913
    ##  8  2013     1     1      557            600        -3      709
    ##  9  2013     1     1      557            600        -3      838
    ## 10  2013     1     1      558            600        -2      753
    ## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

here's what DOES work:

``` r
filter(flights, month == 11 | month == 12)
```

    ## # A tibble: 55,403 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013    11     1        5           2359         6      352
    ##  2  2013    11     1       35           2250       105      123
    ##  3  2013    11     1      455            500        -5      641
    ##  4  2013    11     1      539            545        -6      856
    ##  5  2013    11     1      542            545        -3      831
    ##  6  2013    11     1      549            600       -11      912
    ##  7  2013    11     1      550            600       -10      705
    ##  8  2013    11     1      554            600        -6      659
    ##  9  2013    11     1      554            600        -6      826
    ## 10  2013    11     1      554            600        -6      749
    ## # ... with 55,393 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

and alternatively:

``` r
filter(flights, month %in% c(11, 12))
```

    ## # A tibble: 55,403 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013    11     1        5           2359         6      352
    ##  2  2013    11     1       35           2250       105      123
    ##  3  2013    11     1      455            500        -5      641
    ##  4  2013    11     1      539            545        -6      856
    ##  5  2013    11     1      542            545        -3      831
    ##  6  2013    11     1      549            600       -11      912
    ##  7  2013    11     1      550            600       -10      705
    ##  8  2013    11     1      554            600        -6      659
    ##  9  2013    11     1      554            600        -6      826
    ## 10  2013    11     1      554            600        -6      749
    ## # ... with 55,393 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

``` r
#this is the first time we see %in%
#select every row where [x] is one of the values in the c() grouping. 
```

and because that works and it looks like the book wants to use it later:

``` r
nov_dec <- filter(flights, month %in% c(11, 12))
```

missing values
--------------

``` r
# Let x be Mary's age. We don't know how old she is.
x <- NA

# Let y be John's age. We don't know how old he is.
y <- NA

# Are John and Mary the same age?
x == y
```

    ## [1] NA

``` r
#> [1] NA
# We don't know!
```

If you want to determine if a value is missing, use is.na():

``` r
is.na(x)
```

    ## [1] TRUE

*filter() only includes rows where the condition is TRUE*

exercises:
----------

Find all flights that:

1.  Had an arrival delay of two or more hours

``` r
#we need the flights data
flights %>% 
  #and arrival delay is in minutes, so filter that to greater than 120 minutes
  filter(arr_delay >= 120) 
```

    ## # A tibble: 10,200 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      811            630       101     1047
    ##  2  2013     1     1      848           1835       853     1001
    ##  3  2013     1     1      957            733       144     1056
    ##  4  2013     1     1     1114            900       134     1447
    ##  5  2013     1     1     1505           1310       115     1638
    ##  6  2013     1     1     1525           1340       105     1831
    ##  7  2013     1     1     1549           1445        64     1912
    ##  8  2013     1     1     1558           1359       119     1718
    ##  9  2013     1     1     1732           1630        62     2028
    ## 10  2013     1     1     1803           1620       103     2008
    ## # ... with 10,190 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

1.  Flew to Houston (IAH or HOU)

``` r
flights %>% 
  filter(dest %in% c("IAH", "HOU"))
```

    ## # A tibble: 9,313 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1  2013     1     1      517            515         2      830
    ##  2  2013     1     1      533            529         4      850
    ##  3  2013     1     1      623            627        -4      933
    ##  4  2013     1     1      728            732        -4     1041
    ##  5  2013     1     1      739            739         0     1104
    ##  6  2013     1     1      908            908         0     1228
    ##  7  2013     1     1     1028           1026         2     1350
    ##  8  2013     1     1     1044           1045        -1     1352
    ##  9  2013     1     1     1114            900       134     1447
    ## 10  2013     1     1     1205           1200         5     1503
    ## # ... with 9,303 more rows, and 12 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

1.  Were operated by United, American, or Delta

2.  Departed in summer (July, August, and September)
3.  Arrived more than two hours late, but didn’t leave late
4.  Were delayed by at least an hour, but made up over 30 minutes in flight
5.  Departed between midnight and 6am (inclusive)
6.  Another useful dplyr filtering helper is between(). What does it do? Can you use it to simplify the code needed to answer the previous challenges?
7.  How many flights have a missing dep\_time? What other variables are missing? What might these rows represent?

Why is NA ^ 0 not missing? Why is NA | TRUE not missing? Why is FALSE & NA not missing? Can you figure out the general rule? (NA \* 0 is a tricky counterexample!)
