---
title: "SourmashProj1"
author: "Hannah Houts"
date: "November 15, 2019"
output: 
  html_document:
    keep_md: yes
    theme: spacelab
---


```r
library(tidyverse)
```

```
## -- Attaching packages ------------------------------------------------ tidyverse 1.2.1 --
```

```
## v ggplot2 3.1.0       v purrr   0.2.5  
## v tibble  2.0.1       v dplyr   0.8.0.1
## v tidyr   0.8.2       v stringr 1.3.1  
## v readr   1.3.1       v forcats 0.3.0
```

```
## -- Conflicts --------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(ggfortify)
```

```
## Warning: package 'ggfortify' was built under R version 3.5.3
```






```r
# Read data into R
comp_mat <- read.csv("CompCSVs/bacteroides_k31_genomic_comp.csv")


#reduce csv col names
colnames(comp_mat) <- sub("X2018.test_datasets.bacteroides.genomic.GCA_", "", colnames(comp_mat))
colnames(comp_mat) <- sub("_genomic.fna.gz_", "", colnames(comp_mat))


  # Set row labels
rownames(comp_mat) <- colnames(comp_mat)
# Transform for plotting
comp_mat <- as.matrix(comp_mat)


autoplot(comp_mat)
```

```
## Scale for 'y' is already present. Adding another scale for 'y', which
## will replace the existing scale.
```

![](SourmashProj1MD_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
#autoplot(cmdscale(eurodist, eig = TRUE))


# Make an MDS plot
fit <- dist(comp_mat)
fit <- cmdscale(fit)
plot(-fit[ , 2] ~ fit[ , 1],
      xlab = "Dim 1",
      ylab = "Dim 2",
      xlim= c(-.6, .9),
      main = "sourmash Compare MDS")
# add labels to the plot
text(fit[ , 2]~ fit[ , 1],
      labels = row.names(fit),
      pos = 4, font = 1,
      data = fit,
      col = c("blue", "blue",
               "orange", "orange"))
```

![](SourmashProj1MD_files/figure-html/unnamed-chunk-2-2.png)<!-- -->



```r
 # Set row labels
rownames(comp_mat) <- colnames(comp_mat)
# Transform for plotting
comp_mat <- as.matrix(comp_mat)
# Make an MDS plot
fit <- dist(comp_mat)
fit <- cmdscale(fit)
plot(-fit[ , 2] ~ fit[ , 1],
      xlab = "Dim 1",
      ylab = "Dim 2",
      xlim= c(-.6, .9),
      main = "sourmash Compare MDS")
# add labels to the plot
text(fit[ , 2]~ fit[ , 1],
      labels = row.names(fit),
      pos = 4, font = 1,
      data = fit,
      col = c("blue", "blue",
               "orange", "orange"))
```

![](SourmashProj1MD_files/figure-html/unnamed-chunk-3-1.png)<!-- -->



```r
autoplot(comp_mat)
```

```
## Scale for 'y' is already present. Adding another scale for 'y', which
## will replace the existing scale.
```

![](SourmashProj1MD_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
#autoplot(cmdscale(eurodist, eig = TRUE))
```


```r
for k in 7 9 12
    do
   for org in bacteroides gingivalis denticola
       do
        for mol in proteomic
            do 
```
