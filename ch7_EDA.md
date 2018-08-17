ch7\_eda
================
jason grahn
8/16/2018

7 Exploratory Data Analysis
===========================

7.1 Introduction
----------------

From the text:

"This chapter will show you how to use visualisation and transformation to explore your data in a systematic way... EDA is an iterative cycle. You:

    1. Generate questions about your data.
    2. Search for answers by visualising, transforming, and modelling your data.
    3. Use what you learn to refine your questions and/or generate new questions.

During the initial phases of EDA you should feel free to investigate every idea that occurs to you... EDA is an important part of any data analysis, even if the questions are handed to you on a platter, because you always need to investigate the quality of your data. Data cleaning is just one application of EDA: you ask questions about whether your data meets your expectations or not. To do data cleaning, you’ll need to deploy all the tools of EDA: visualisation, transformation, and modelling."

### 7.1.1 Prerequisites

primary use of dplyr and ggplot2 in this chapter, load the tidy!

``` r
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.0.0     ✔ purrr   0.2.5
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.6
    ## ✔ tidyr   0.8.1     ✔ stringr 1.3.1
    ## ✔ readr   1.1.1     ✔ forcats 0.3.0

    ## Warning: package 'dplyr' was built under R version 3.5.1

    ## ── Conflicts ─────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

### 7.2 Questioning

"Far better an approximate answer to the right question, which is often vague, than an exact answer to the wrong question, which can always be made precise.” — John Tukey"

EDA is here to understand the data! EDA is a creative process. There are two main types of questions:

    1. What type of variation occurs within my variables?
    2. What type of covariation occurs between my variables? 

define some terms:

    A *variable* is a quantity, quality, or property that you can measure.
    A *value* is the state of a variable when you measure it. The value of a variable may change from measurement to measurement.
    An *observation* is a set of measurements made under similar conditions (you usually make all of the measurements in an observation at the same time and on the same object). An observation will contain several values, each associated with a different variable. I’ll sometimes refer to an observation as a data point.
    *Tabular data* is a set of values, each associated with a variable and an observation. Tabular data is tidy if each value is placed in its own “cell”, each variable in its own column, and each observation in its own row.
