---
title: "Part II"
author: Monty Reynolds 
weight: 2
subtitle: "Selection and Representation."
date: 2021-01-26
draft: false
links:
- icon: campground
  icon_pack: fas
  name: slides
  url: "/slides/06-why-hugo.html"
- icon: hiking
  icon_pack: fas
  name: activity
  url: "collection/day02/06-hugo/#activity" 
---

* How do we select collections of text, and how do we see these results as a representation?:
	* Principles of selection and representation
	* selecting documents:
		* bag of words approach
		* multinominal language model
		* vector space model and similarity metrics
	* distributed representations of words from language sequences

1. How to select the core constructs of a distant-reading inquiry.
2. How to operationalize these constructs for querying the Nietzsche Source.
3. Walk through the methodology for conducting systematic queries that can be reproduced by other researchers.

### 2.4 querying the Nietzsche Source

How to determine which writings to include: [The Window]

The window frames the prevalence and co-occurrence of constructs of interest.

Prevalence==if a construct is used frequently, then the author cares about that construct. This may not say why the author cares about the construct based on the *prevalence statistics*.
co-occurrence==if the author uses a word with another then the author probably associates those constructs.

The value of each rests on the view that both sets of statistics have because if a commentator claims that Nietzsche discusses a construct, the claim can be easily verified or falsified by prevalence statistics. If a commentator claims that Nietzsche associates (negative or positive) two constructs, then they should co-occur often or not. Conversely, if a pair of constructs does co-occur often, that is strong evidence that ther eis some conceptual or inferential relation between them. Additionally, both prevalence statistics and co=occurrence statistics can be used to test and discover hypotheses about periodization.

There is, however, no hard and fast rule for determining what counts for prevalence or co-occurrence because there is no hard and fast rule for determining the amount of text that falls within a given unit of analysis. What is a unit of analysis? Is the *window*?

### 2.5 Cleaning the Data

How to prepare the data for visualization: for opimal use in visual and statistics analytics applications, one must arrange them in a precise tabular format and then transform them for the application in question.

*Data structure for cleaning query results from the Nietzsche Source* In this case it is the preface and first thirteen numbered sections of *The Antichrist*.

* Each row below is a is a single passage in one of Nietzsche's texts. (3,321)
* The columns represent the bibliographic details (book, passage number or title, order within the book, year of publication)
* sections 1 and 2 refer to both *virtue* and *value*, but not to *type* or *drive*. Section 7 refers to *instinct*, *virtue*, and *value*.
* the full spreadsheet has several thousand rows and represents the "presence or absence of the forty-seven constructs cataloged in Table 2.1."
 
#### Table 2.2 (representative sample):

| Book | Section | Order | Year | Type | Exemplar | Drive | Instinct | Virtue | Value |
|------|---------|-------|------|------|----------|-------|----------|--------|-------|
| A    | P       | 1     | 1888 | 0    | 0        | 0     | 0        | 0      | 0     |
| A    | 1       | 2     | 1888 | 0    | 0        | 0     | 0        | 1      | 0     |
| A    | 2       | 3     | 1888 | 0    | 0        | 0     | 0        | 1      | 0     |
| A    | 3       | 4     | 1888 | 1    | 0        | 0     | 0        | 0      | 0     |
| ...  |         |       |      |      |          |       |          |        |       |
| A    | 7       | 8     | 1888 | 1    | 0        | 0     | 1        | 1      | 1     |

* Prevalence within a book or a whole corpus is calculated by summing a column.
* A semantic network is a network of associations between two or more constructs, where they *co-occur* when the columns associated with them both have a "1" in the same row.
* To create semantic networks, Alphano uses Gephi. Data is uploaded to Gephi in a dataset format called an *adjacency matrix* (Breiger 1974). This is done creating another spreadsheet that contains the matrix multiplication of the original dataset by its trasnpose. This generates an array of pairwise overlaps between constructs (adjacency matrix)

#### Table 2.3 (representative sample)

| -        | Type | Exemplar | Drive | Instinct | Virtue | Value | Nobility |
|----------|------|----------|-------|----------|--------|-------|----------|
| Type     | 136* | 3        | 15    | 61       | 27     | 59    | 23       |
| Exemplar | 3    | 11*      | 2     | 2        | 4      | 4     | 4        |
| Drive    | 15   | 2        | 152*  | 32       | 31     | 43    | 18       |


