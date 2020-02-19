
<!-- README.md is generated from README.Rmd. Please edit that file -->

# <img src="https://i.imgur.com/3jITMq8.png" align="right" height=40 /> Match loanbook with asset level data

<!-- badges: start -->

[![lifecycle](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
[![CRAN
status](https://www.r-pkg.org/badges/version/r2dii.match)](https://CRAN.R-project.org/package=r2dii.match)
[![Travis build
status](https://travis-ci.org/2DegreesInvesting/r2dii.match.svg?branch=master)](https://travis-ci.org/2DegreesInvesting/r2dii.match)
[![Coveralls test
coverage](https://coveralls.io/repos/github/2DegreesInvesting/r2dii.match/badge.svg)](https://coveralls.io/r/2DegreesInvesting/r2dii.match?branch=master)
[![Codecov test
coverage](https://codecov.io/gh/2degreesinvesting/r2dii.match/branch/master/graph/badge.svg)](https://codecov.io/gh/2degreesinvesting/r2dii.match?branch=master)
[![R build
status](https://github.com/2DegreesInvesting/r2dii.match/workflows/R-CMD-check/badge.svg)](https://github.com/2DegreesInvesting/r2dii.match/actions)
<!-- badges: end -->

The goal of r2dii.match is to match counterparties from a generic
loanbook data with physical asset level data (ald).

## Installation

Before you install r2dii.match you may want to:

  - [Try an rstudio.cloud project that has r2dii.match already
    installed](https://rstudio.cloud/project/954051).
  - [Learn how to minimize installation
    errors](https://gist.github.com/maurolepore/a0187be9d40aee95a43f20a85f4caed6#installation).

When you are ready, install the development version of r2dii.match from
GitHub with:

``` r
# install.packages("devtools")
devtools::install_github("2DegreesInvesting/r2dii.match")
```

## Example

``` r
library(r2dii.match)
library(r2dii.dataraw)
#> Loading required package: r2dii.utils
suppressPackageStartupMessages(
  library(tidyverse)
)
```

Matching is achieved in two main steps:

### 1\. Run fuzzy matching

`match_name()` will extract all unique counterparty names from the
columns: `direct_loantaker`, `ultimate_parent` or `intermediate_parent*`
and run fuzzy matching against all company names in the `ald`:

``` r
match_result <- match_name(loanbook_demo, ald_demo)
match_result 
```

### 2\. Prioritize validated matches

The user should then manually validate `match_result`, ensuring that the
`score` value is only equal to `1` for perfect matches. Once validated,
the `prioritize()` function, will choose only the valid matches,
prioritizing (by default) `direct_loantaker` matches over
`ultimate_parent` matches:

``` r
priotize(match_result)
```

The result is a dataset, with identical columns to the input loanbook,
and added columns bridging all matched loans to their ald counterpart.

For a more detailed walkthrough of the functionality [see the
documentation](https://2degreesinvesting.github.io/r2dii.match/articles/r2dii.match.html)
