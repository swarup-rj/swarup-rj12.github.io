---
title: "Text Mining in R: Data Processing"
layout: post
date: 2020-07-30
tags: blog
comments: true
---
###### Goal
* To demonstrate the processing of data in R for further text analysis.

###### Import dependencies
```r
# Load packages
library("RCurl")
library("XML")
library("tidyverse")
```

###### Load the data
Download the dataset: [200 text Commentaries for batsman Steve Smith](https://swarup-rj.github.io/assets/data/SmithCommentary200.csv)
```r
commentary200 <- read.csv("SmithCommentary200.csv", stringsAsFactors = FALSE)
```

```r
dim(commentary200)
#[1] 200   3
str(commentary200)
#'data.frame':   200 obs. of  3 variables:
#$ info      : chr  " umar gul to smith 1 no ball " " umar gul to smith no run" " umar gul to smith no run" " umar gul to smith no run" ...
#$ commentary: chr  " gets another no ball from gul first up apart from that it was a good delivery yorker that smith just jabbed a "| __truncated__ " this is better in the sense that it was a legal delivery but worse in terms of line giving smith an early chan"| __truncated__ " this was a touch wide again but not as wide as guls smile after he saw this bend away late big reverse swing w"| __truncated__ " gets the line right perhaps its a touch too short though and smith gets behind a solid defence " ...
#$ response  : int  1 0 0 0 0 0 -1 1 0 0 ...
```
###### Filter the data
Remove text Commentaries shorter than 10 characters
```r
commentary200 <- commentary200[nchar(commentary200$commentary) > 10, ]
dim(commentary200)
#[1] 198   3
```
