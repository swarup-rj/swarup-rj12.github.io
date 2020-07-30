---
title: "Text Mining in R: Data Preprocessing"
layout: post
date: 2020-07-30
tags: blog
comments: true
---
###### Goal
* To demonstrate the processing of data in R for further text analysis.

###### Load the data
Download the dataset: [200 text Commentaries for batsman Steve Smith](https://swarup-rj.github.io/assets/data/SmithCommentary200.csv)
```r
commentary200 <- read.csv("SmithCommentary200.csv", stringsAsFactors = FALSE)
```

```r
dim(commentary200)
#[1] 200   3
str(commentary200)
# data.frame:   200 obs. of  3 variables:
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

###### Data Tokenization and Stemming
```r
library(SnowballC)
library(tidytext)
library(hunspell)
library(dplyr)

# tokenize the commentary
comm.tm <- unnest_tokens(commentary200, word, commentary, to_lower = TRUE)

# “go”, “goes”, “going”, and “gone” ----mutate----> “go”
comm.tm <- mutate(comm.tm, word.stem = wordStem(word, language = "en"))

# steming function
stem_hunspell <- function(term) {
    stems <- hunspell_stem(term)[[1]]
    
    if (length(stems) == 0) {
        stem <- NA
    } else {
        if (nchar(stems[[length(stems)]]) > 1) 
            stem <- stems[[length(stems)]] else stem <- term
    }
    stem
}

word.list <- count(comm.tm, word)

# find the stems of the words
words.stem <- lapply(word.list$word, stem_hunspell)

# save to file and manually check the words
stem.list <- cbind(word.list, stem = unlist(words.stem))
stem.list <- stem.list[!is.na(stem.list[, 3]) & stem.list[, 1] != stem.list[, 3],]
write.csv(stem.list, "stem.list.commentary.csv", row.names = F)

# replace the words in the commentaries with the selected stems
stem.list <- read.csv("stem.list.commentary.csv", stringsAsFactors = FALSE)
comm.stem <- commentary200
orig.words <- paste0("\\b", stem.list[, 1], "\\b")
stem.words <- stem.list[, 3]
comm.stem$commentary <- stri_replace_all_regex(comm.stem$commentary, orig.words, stem.words, vectorize_all = FALSE)

# remove duplicates
comm.stem <- comm.stem[!duplicated(comm.stem$commentary), ]

# Save the final stemmed commentary for further use
write.csv(comm.stem, "commentary200.stem.commentary.csv", row.names = F)
```
