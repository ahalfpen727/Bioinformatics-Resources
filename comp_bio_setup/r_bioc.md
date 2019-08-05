# Set up R, RStudio, and Bioconductor

It's important to have the latest software in Computational Biology
which means updating software often. Bioconductor, for example, has
new releases every 6 months (April and October every year).

## R

Start by downloading the latest version of R which can be found by
following the "Download R" links at the top of the page here:

<https://cran.r-project.org/>

## RStudio

Next download the free RStudio Desktop program for using R:

<https://www.rstudio.com/products/RStudio/>

## Bioconductor

Now, load up RStudio. To install Bioconductor, you type the following
lines of code into the R shell:

```{r}
source("http://bioconductor.org/biocLite.R")
biocLite()
```

If this finishes without an error, you're set up.

