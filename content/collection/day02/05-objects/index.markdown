---
title: "R Objects and Commands"
author: Montaque Reynolds 
weight: 5
subtitle: "3 types of R objects, vector, data frame, and matrix."
date: 2021-01-26
draft: false
links:
- icon: campground
  icon_pack: fas
  name: slides
  url: "/slides/05-why-netlify.html"
- icon: hiking
  icon_pack: fas
  name: activity
  url: "collection/day02/05-netlify/#activity"
---



## Vectors

Contains a set of values. These include `vec_num`, number vector and `vec_char` whwhich is a character vector. `c()` combines the elements of a vector and `<-` assigns a vector to a variable.


```r
vec_num <- c(1, 5, 6, 3)
vec_num
```


```r
vec_char <- c("apple", "banana", "mandarin", "melon")
vec_char
```

Once we have created a vector, we can extract its elements using the `[]` operator. For instance, you can extract the first element `[1]`, 


```r
vec_char <- c("apple", "banana", "mandarin", "melon")
vec_char[1]
```

or the first 4 elements `[1:5]`.


```r
vec_char[1:4]
```

