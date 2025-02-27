
<!-- README.md is generated from README.Rmd. Please edit that file -->

# miniCRAN <img src='man/figures/miniCRAN-logo.png' align="right" height="139" />

<!-- badges: start -->

[![Build
Status](https://travis-ci.org/andrie/miniCRAN.svg?branch=master)](https://travis-ci.org/andrie/miniCRAN)
[![Codecov test
coverage](https://codecov.io/gh/andrie/miniCRAN/branch/master/graph/badge.svg)](https://codecov.io/gh/andrie/miniCRAN?branch=master)
[![CRAN
version](http://www.r-pkg.org/badges/version/miniCRAN)](http://www.r-pkg.org/pkg/miniCRAN)
[![CRAN RStudio mirror
downloads](http://cranlogs.r-pkg.org/badges/miniCRAN)](http://www.r-pkg.org/pkg/miniCRAN)
[![CRAN
status](https://www.r-pkg.org/badges/version/miniCRAN)](https://cran.r-project.org/package=miniCRAN)
<!-- badges: end -->

Create a mini version of CRAN containing only selected packages

## Introduction

At the end of 2014, CRAN consisted of more than 6,000 packages, and by
2017 this number doubled to more than 12,000. Many organisations need to
maintain a private mirror of CRAN, but with only a subset of packages
that are relevant to them.

The `miniCRAN` package makes it possible to create an internally
consistent repository consisting of selected packages from CRAN-like
repositories. The user specifies a set of desired packages, and
`miniCRAN` recursively reads the dependency tree for these packages,
then downloads only this subset.

## Important functions:

| Function           | Use it for                                                             |
| ------------------ | ---------------------------------------------------------------------- |
| `pkgDep()`         | Find package dependencies                                              |
| `makeRepo()`       | Make repository (with or without downloading packages)                 |
| `addPackage()`     | Add additonal packages (and their dependencies) to existing repository |
| `updatePackages()` | Update the versions of packages currently in the repository            |

## Installation:

Get the stable version from CRAN:

``` r
install.packages("miniCRAN")
library("miniCRAN")
```

### Development version

Get the latest development version from github:

``` r
# Use `devtools` to install directly from github
library(devtools)
install_github("andrie/miniCRAN")
```

### System requirements

The `miniCRAN` package itself doesn’t introduce any system dependencies.
However, the package imports the
[`curl`](https://cran.r-project.org/package=curl) and
[`XML`](https://cran.r-project.org/package=XML) packages. These have
system requirements on `libxml2-devel`, `libcurl-devel` and
`openssl-devel`.

  - On systems with the `rpm` package manager (Red Hat, CentOS) try:

<!-- end list -->

``` bash
yum install libcurl-devel libxml2-devel openssl-devel
```

  - On systems with the `aptitude` package manager (Debian, Ubuntu) try:

<!-- end list -->

``` bash
apt-get install libcurl4-openssl-dev libxml2-devel openssl-devel
```

## Example:

``` r
# Determine and download the packages `ggplot2`, `plyr` and `reshape2`, 
# including their dependencies:

library("miniCRAN")
pkgs <- c("ggplot2", "plyr", "reshape2")
makeRepo(pkgDep(pkgs), path = file.path(tempdir(), "miniCRAN"))
```

## Supported by Microsoft

I started this project while employed by Revolution Analytics and
Microsoft. Microsoft has kindly agreed that I maintain the project
individually, and retains copyright to all work on the project until
October 2017.
