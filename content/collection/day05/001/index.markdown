---
title: "What is Tidy Text?"
author: Montaque Reynolds 
weight: 1
subtitle: "Blah."
date: 2022-06-14
draft: false
---

### What Tidy Text Look Like?

The specific structure of *tidy text* is:

* Each variable is a column
* Each observation is a row
* Each type of observational unit is a table

Below is an example of a character vector:


```r
text <- c("Because I could not stop for Death -",
          "He kindly stopped for me -",
          "The Carriage held but just Ourselves -",
          "and Immortality")

text
```

```
## [1] "Because I could not stop for Death -"  
## [2] "He kindly stopped for me -"            
## [3] "The Carriage held but just Ourselves -"
## [4] "and Immortality"
```

We have taken four character strings; "Because I could not . . ." etc, and stored it in a variable called `text`.

In order to analyze it, we first place it in a frame:


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
text_df <- tibble(line = 1:4, text = text)

text_df
```

```
## # A tibble: 4 × 2
##    line text                                  
##   <int> <chr>                                 
## 1     1 Because I could not stop for Death -  
## 2     2 He kindly stopped for me -            
## 3     3 The Carriage held but just Ourselves -
## 4     4 and Immortality
```

This particular dataframe is called a `tibble`. We use tibbles because they have a convenient method of printing output, will not convert strings to factors (numbers), and do not use row names. However, in this format, we still cannot compare word frequencies etc. This is because each object that we have to work with is a full sentence and therefore does not let us access each word individually. Therefore we need to convert it into a format that allows **one token per document (tokenization)**. We will do this using the `unnest_tokens()` function:


```r
library(tidytext)

text_df %>%
  unnest_tokens(word, text)
```

```
## # A tibble: 20 × 2
##     line word       
##    <int> <chr>      
##  1     1 because    
##  2     1 i          
##  3     1 could      
##  4     1 not        
##  5     1 stop       
##  6     1 for        
##  7     1 death      
##  8     2 he         
##  9     2 kindly     
## 10     2 stopped    
## 11     2 for        
## 12     2 me         
## 13     3 the        
## 14     3 carriage   
## 15     3 held       
## 16     3 but        
## 17     3 just       
## 18     3 ourselves  
## 19     4 and        
## 20     4 immortality
```

Looking at the output shows us three columns. The first is the row of the document, the second comprises the sentence that that particular token belonged to (line), and finally the token itself (word).

In the following, we will begin to manipulate, process, and visualize the text using our set of *tidy* tools: `dplyr`, `tidyr`, and `ggplot2`:

![A flowchart of a typical text analysis using tidy data principles. This chapter shows how to summarize and visualize text using these tools.](/home/redapemusic35/1-2021-22-Projects/Website/CV-Project-Page/static/tdrflowchart.png)

### Tidy Text and Jane Austen


```r
library(janeaustenr) # import jane austen
library(dplyr) # the r package dplyr
library(stringr) # and stringr

original_books <- austen_books() %>% # create a variable to store chapters etc
  group_by(book) %>%
  mutate(linenumber = row_number(),
         chapter = cumsum(str_detect(text, # to find the chapters
                                     regex("^chapter [\\divxlc]",
                                           ignore_case = TRUE)))) %>%
  ungroup()

original_books
```

```
## # A tibble: 73,422 × 4
##    text                    book                linenumber chapter
##    <chr>                   <fct>                    <int>   <int>
##  1 "SENSE AND SENSIBILITY" Sense & Sensibility          1       0
##  2 ""                      Sense & Sensibility          2       0
##  3 "by Jane Austen"        Sense & Sensibility          3       0
##  4 ""                      Sense & Sensibility          4       0
##  5 "(1811)"                Sense & Sensibility          5       0
##  6 ""                      Sense & Sensibility          6       0
##  7 ""                      Sense & Sensibility          7       0
##  8 ""                      Sense & Sensibility          8       0
##  9 ""                      Sense & Sensibility          9       0
## 10 "CHAPTER 1"             Sense & Sensibility         10       1
## # … with 73,412 more rows
```

As we did before, we need to convert it into a **one token per line** format:


```r
library(tidytext)
tidy_books <- original_books %>%
  unnest_tokens(word, text)

tidy_books
```

```
## # A tibble: 725,055 × 4
##    book                linenumber chapter word       
##    <fct>                    <int>   <int> <chr>      
##  1 Sense & Sensibility          1       0 sense      
##  2 Sense & Sensibility          1       0 and        
##  3 Sense & Sensibility          1       0 sensibility
##  4 Sense & Sensibility          3       0 by         
##  5 Sense & Sensibility          3       0 jane       
##  6 Sense & Sensibility          3       0 austen     
##  7 Sense & Sensibility          5       0 1811       
##  8 Sense & Sensibility         10       1 chapter    
##  9 Sense & Sensibility         10       1 1          
## 10 Sense & Sensibility         13       1 the        
## # … with 725,045 more rows
```
