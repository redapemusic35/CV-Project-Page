---
title: "Packages"
weight: 4
subtitle: "Installing needed and useful packages."
links:
- icon: campground
  icon_pack: fas
  name: slides
  url: "/slides/04-why-blog.html"
- icon: hiking
  icon_pack: fas
  name: activity
  url: "collection/day01/04-blog/#activity"
---



First, we are going to install the quanteda package.


```r
install.packages("quanteda")
```

We will also need to load the following functions separately: `install.packages("quanteda.textmodels")
install.packages("quanteda.textstats")
install.packages("quanteda.textplots")`


```r
install.packages("quanteda.textmodels")
install.packages("quanteda.textstats")
install.packages("quanteda.textplots")
```

We also use the `readtext` package to read in `txt` files.


```r
install.packages("readtext")
```

Some of the tutorials we will look at are in the `quanteda.corpora` package.


```r
install.packages("devtools") # get devtools to install quanteda.corpora
devtools::install_github("quanteda/quanteda.corpora")
```

Some other useful packages that we should download


```r
install.packages("spacyr")
```

Spacy will enable functions such as part-of-speech tagging, entity-recognition, and dependency parsing.

Also, we should download


```r
install.packages("newsmap")
install.packages("seededlda")
```

In summary, the packages that we will use and should have installed include:

```
require(quanteda)
require(quanteda.textmodels)
require(quanteda.textstats)
require(quanteda.textplots)
require(readtext)
require(devtools)
require(quanteda.corpora)
require(newsmap)
require(seededlda)
```

