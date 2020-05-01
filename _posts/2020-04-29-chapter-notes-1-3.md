---
title: "Chapter Notes 1-3"
date: 2020-04-29 # Added
tags: [bayesian, statistical rethinking, notes]
header:
  image: "/images/fort point.png"
exerpt: "My chapter notes"
output:
  md_document:
    variant: markdown_github
mathjax: "true"
comments: "true"
# output:
#  html_document:
#   keep_md: true
# mathjax: "true"
---

This is a test 

```r
knitr::opts_chunk$set(echo = TRUE)
# install.packages(c("code", "mvtnorm", "devtoosl", "loo"))
# library(devtools)
# devtools::install_github("rmcelreath/rethinking",
                         # ref="Experimental")
library(rethinking)
library(ggplot2)
library(magrittr)
library(dplyr)
library(cowplot)
```

# Grid Approximation
```r
# Step 1: Define the grid, what are all the values you're going to consider
p_grid <- seq(from=0, to=1, length.out = 1000)

# Step 2: Define the prior: Assume uniform and assign 1 to every value of p we're considering. We assign 1 so that the integral sums to 1
prob_p <- rep(1, 1000)

# Step 3: Get the probability of the data, aka, the likelihood. 6 waters, 9 tosses
prob_data <- dbinom(6, size=9, prob=p_grid)

# Step 4: Computer the posterior
posterior <- prob_data * prob_p

# Step 5: Standardize the posterior
posterior <- posterior / sum(posterior)

plot(p_grid, posterior, type = "b",
     xlab = "probability of water",
     ylab = "posterior probability")
mtext("1000 points")
```
