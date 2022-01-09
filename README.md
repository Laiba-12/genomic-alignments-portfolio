# genomic-alignments-portfolio
---
title: "Genomic Alignments"
author: "Laiba Khalid"
date: "07/01/2022"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Introduction:

Provides efficient storage and manipulation containers for small “genomic alignments (typically obtained by aligning short reads to a reference genome)”. This covers “read counting”, “coverage computation”,” junction identification”, and “alignment nucleotide content manipulation”(Lawrence et al. 2013).

Genomic Alignments is a package within the Bioconductor project in R.
This package is used as a starting point for representation of genomic alignments in R. In this package, it is based on the infrastructure of genomes and it indulges with most of the bioconductor packages.
Three categories are defined here: “GAlignments”, “GAlignmentPairs”, and “GAlignmentList”,representing, “genomic alignments”, “pairs of genomic alignments” and “groups of genomic alignments” respectively.
“GenomicAlignments”  is accessible at “bioconductor.org” and can be downloaded by following this command:

```{r}
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("GenomicAlignments")

library(GenomicAlignments)

```


## GAlignments:
A class as a container that is used to store a set of genomic alignments. It supports “ Binary Alignment Map” or “BAM” files. It also indulges with alignments in the reference sequence with gaps, for instance, from “RNA-seq experiment” that stores junction reads to make the class.
So, it’s a “vector-like object” that explains an alignment, means “how a given sequence aligns to reference sequence”.

GAlignments object can be generated from a “BAM” file.
In this scenario, each element in the generated object corresponds to a file record. One thing to keep in mind is that the object does not have all of the information contained in the “BAM/SAM records”. For the time being, we'll ignore “query sequences (SEQ field)”, “query ids (QNAME field)”, “query qualities (QUAL)”, “mapping qualities (MAPQ)”, and any other data that isn't required to enable the actions specified in this text. This also implies that multi-reads (i.e. reads with multiple hits in the reference) are not treated differently, and the numerous “SAM/BAM records” corresponding to a multi-read will appear in the GAlignments object as if they came from separate searches.


## SAM tools:
 "Sequence Alignment/Map (SAM) format" is a general alignment format for storing read alignments against reference sequences, and it contains both “short and long reads (up to 128 Mbp)” generated by various sequencing systems(Li et al.). SAMtools provides universal tools for processing read alignments in the SAM format, such as “indexing”,” variant caller”, and “alignment viewer”(Li et al.).
## Import BAM file into GAlignments object:
A function which is readGAlignments is used to load a BAM file in selected object.

```{r}
library(GenomicAlignments)
aln1_file <- system.file("extdata", "ex1.bam", package="Rsamtools")
aln1 <- readGAlignments(aln1_file)
aln1
```
```{r}
length(aln1)
```
"So, it means 3271 BAM records were loaded into GAlignments".

## "Simple Accessor methods":
The show methods display one accessor per field, that contains “same name as the field”. "They all return as same factor as the item".

```{r}
head(seqnames(aln1))
```
```{r}
seqlevels(aln1)
```
```{r}
head(strand(aln1))
```
```{r}
head(start(aln1))
```
```{r}
head(end(aln1))
```
```{r}
head(njunc(aln1))
```
## Discussion
Biocoductor infrastructure is used in a computationalenvironment on “annotated genomic ranges”,as well as integrating “genomic data with R” and its extensions' statistical computing capabilities. Three packages make foundation of the basic features: “IRanges, GenomicRanges, and GenomicFeatures”. These programmes offer scalable data structures for describing annotated genome ranges, including, “read alignments”, and “coverage vectors”. More than 80% Bioconductor programmes, such as for “sequence analysis”,” differential expression analysis”, and visualisation, are directly supported by this infrastructure.
In future, the class of GAlignmentpairs and GAlignmentlist will be available with precise methods.Finally, as datasets grow in size, we can execute more efficient algorithms and data structures, as well as ways to take use of parallel processing(Lawrence et al. 2013).


## References:

```{r}
 citation("GenomicAlignments")
```

Durbin, R. and Durbin, R. The Sequence Alignment/Map format and SAMtools.  (1367-4811 (Electronic)).
er, N., Homer N Fau - Marth, G., Marth G Fau - Abecasis, G., Abecasis G Fau 

Lawrence, M., Huber, W., Pagès, H., Aboyoun, P., Carlson, M., Gentleman, R., Morgan, M. T. and Carey, V. J. (2013) Software for Computing and Annotating Genomic Ranges. PLOS Computational Biology 9 (8), e1003118.


Li, H., Handsaker B Fau - Wysoker, A., Wysoker A Fau - Fennell, T., Fennell T Fau - Ruan, J., Ruan J Fau - Hom
