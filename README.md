MOSAIC on scNMT\_seq Mouse Gastrulation data
================

## Introduction

We will be analyzing
[scNMT-seq](https://www.nature.com/articles/s41467-018-03149-4) study
via MOSAIC to understand mouse gastrulation on their epigenome and
transcriptome profiles to identify multi-omics signatures that
characterize stage and lineage.

[MOSAIC](https://github.com/arorarshi/MOSAIC) or Multi-Omics Supervised
Integrative Clustering is a response weighted clustering algorithm
inspired by [survClust](https://github.com/arorarshi/survClust), to
classify samples into clusters that are relevant to outcome of
interest.<sup>1</sup>

Each feature in a data type is weighed according to its association with
binary or categorical outcome of interest, and a weighted distance
matrix is computed <sup>2</sup>. This reduces the computation space
considerably from sample x feature to sample x sample. Samples are then
projected into a multi dimensional space preserving the distance between
them, and clustered with k-means algorithm to obtain class labels
corresponding to outcome.

## Analysis

    ## [[1]]
    ## [1] "stage"
    ## 
    ## [[2]]
    ## [1] "lineage.all"
    ## 
    ## [[3]]
    ## [1] "lineage"
    ## 
    ## [[4]]
    ## [1] "cv.stats"

We ran MOSAIC for *50 rounds* of *5-fold* cross validation for *k=2-7*,
with stage and lineage as outcome of interest over 13 data types - \*
RNA \* met\_CTCF, met\_DHS, met\_p300, met\_genebody, met\_promoter,
met\_cgi \* acc\_CTCF, acc\_DHS, acc\_p300, acc\_genebody,
acc\_promoter, acc\_cgi

and integrating all of them, to mine features that are associated with
outcome of interest.

RNA data was standardized, whereas proportion data from other data types
was first transformed by taking their folded square root before
standardizing.

All the data was considered, including missing-ness, as MOSAIC can
handle incomplete information among features and data types. If a data
type had more than 5000 features, teh feature space was reduce to top
5000 most variable features.

Let’s take a look at stage and lineage distribution.

<table>

<caption>

sample summary

</caption>

<tbody>

<tr>

<td style="text-align:left;">

stage=E4.5

</td>

<td style="text-align:left;">

104(12.59%)

</td>

</tr>

<tr>

<td style="text-align:left;">

E5.5

</td>

<td style="text-align:left;">

108(13.08%)

</td>

</tr>

<tr>

<td style="text-align:left;">

E6.5

</td>

<td style="text-align:left;">

271(32.81%)

</td>

</tr>

<tr>

<td style="text-align:left;">

E7.5

</td>

<td style="text-align:left;">

343(41.53%)

</td>

</tr>

</tbody>

</table>

    ##       y
    ## x      Ectoderm Endoderm Epiblast ExE_ectoderm Mesoderm Primitive_endoderm
    ##   E4.5        0        0       60            0        0                 43
    ##   E5.5        0        0       84            0        0                  0
    ##   E6.5        0        0      146            8       28                  0
    ##   E7.5       43       81       44            0      141                  0
    ##       y
    ## x      Primitive_Streak Visceral_endoderm <NA>
    ##   E4.5                0                 0    1
    ##   E5.5                0                24    0
    ##   E6.5               43                45    1
    ##   E7.5               33                 0    1

<table>

<caption>

stage vs lineage

</caption>

<thead>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

Ectoderm

</th>

<th style="text-align:right;">

Endoderm

</th>

<th style="text-align:right;">

Epiblast

</th>

<th style="text-align:right;">

ExE\_ectoderm

</th>

<th style="text-align:right;">

Mesoderm

</th>

<th style="text-align:right;">

Primitive\_endoderm

</th>

<th style="text-align:right;">

Primitive\_Streak

</th>

<th style="text-align:right;">

Visceral\_endoderm

</th>

<th style="text-align:right;">

NA

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

E4.5

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

60

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

43

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

1

</td>

</tr>

<tr>

<td style="text-align:left;">

E5.5

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

84

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

24

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

E6.5

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

146

</td>

<td style="text-align:right;">

8

</td>

<td style="text-align:right;">

28

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

43

</td>

<td style="text-align:right;">

45

</td>

<td style="text-align:right;">

1

</td>

</tr>

<tr>

<td style="text-align:left;">

E7.5

</td>

<td style="text-align:right;">

43

</td>

<td style="text-align:right;">

81

</td>

<td style="text-align:right;">

44

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

141

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

33

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

1

</td>

</tr>

</tbody>

</table>

## Results

We analyze MOSAIC obtained cross validated solutions over two metrics -
adjusted Mutual Information (AMI) and Standardized Pooled Within Sum of
Squares (SPWSS)

### Stage

<img src="README_figures/README-unnamed-chunk-3-1.png" width="1056" />

## References

1.  Arora A, Olshen AB, Seshan VE, and Shen R. Pan-cancer identification
    of clinically relevant genomic subtypes using outcome-weighted
    integrative clustering. Biorxiv

2.  Xing, E. P., Jordan, M. I., Russell, S. J., & Ng, A. Y. (2003).
    Distance metric learning with application to clustering with
    side-information. In Advances in neural information processing
    systems (pp. 521-528).
