
<!-- README.md is generated from README.Rmd. Please edit that file -->

# here

<!-- badges: start -->

[![Travis-CI Build
Status](https://travis-ci.org/r-lib/here.svg?branch=master)](https://travis-ci.org/r-lib/here)
[![CRAN
status](https://www.r-pkg.org/badges/version/here)](https://CRAN.R-project.org/package=here)
[![Lifecycle:
stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://www.tidyverse.org/lifecycle/#stable)
<!-- badges: end -->

The goal of the here package is to enable easy file referencing. In
contrast to using `setwd()`, which is fragile and dependent on the way
you organize your files, here uses the top-level directory of a project
to easily build paths to files.

## Installation

Install the released version of here from CRAN:

``` r
install.packages("here")
```

Or install the development version from GitHub with:

``` r
devtools::install_github("r-lib/here")
```

## Usage

The here package creates paths relative to the top-level directory. The
package displays the top-level of the current project on load or any
time you call `here()`:

``` r
library(here)
#> here() starts at /Users/sharla/github/tidy-dev-day-2020/here
here()
#> [1] "/Users/sharla/github/tidy-dev-day-2020/here"
```

You can build a path relative to the top-level directory in order to
read or write a file:

``` r
here("files", "data", "iris.csv")
```

``` r
write.csv(iris, here("files", "data", "iris.csv"))
```

This works regardless of where the associated source file lives inside
your project. This is especially helpful if you use RMarkdown with the
default behaviour, where the working directory is the directory where
the file is.

Consider the following directory:

    ├── analysis
    │   └── report.Rmd
    ├── data
    │   └── data.csv
    ├── project.Rproj

The working directory is for `report.Rmd` is the `analysis/`
subdirectory, while `data.csv` lives in the `data/` subdirectory.

To render `report.Rmd`, you would have to ensure the path to `data.csv`
is relative to the `analysis/` directory - i.e., `../data/data.csv`. The
chunks would knit properly, but could not be run in the console since
the working directory in the console *isn’t* `analysis/`.

The here package circumvents this issue by always creating the file path
relative to the top level directory, so that `data.csv` can be read
using `here("data", "data.csv")` both when the report is knit and when
the code is run interactively in the
console.

![](/Users/sharla/github/tidy-dev-day-2020/here/man/figures/illustration.png)<!-- -->
*Illustration by [Allison Horst](https://github.com/allisonhorst)*
