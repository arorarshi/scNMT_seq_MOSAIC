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

We ran MOSAIC for **50 rounds** of **5-fold** cross validation for
**k=2-7**, with stage and lineage as outcome of interest over 5 data
types -

  - RNA
  - met\_DHS, met\_genebody, met\_promoter, met\_cgi

and integrating all of them, to mine features that are associated with
outcome of interest.

RNA data was standardized, whereas proportion data from other data types
was first transformed by taking their folded square root before
standardizing.

All the data was considered, including missing-ness, as MOSAIC can
handle incomplete information among features and data types. If a data
type had more than 5000 features, the feature space was reduce to top
5000 most variable features.

Let’s take a look at stage and lineage distribution.

We removed samples belonging to Embryonic Lineage, see lineage table
below

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

63(7.88%)

</td>

</tr>

<tr>

<td style="text-align:left;">

E5.5

</td>

<td style="text-align:left;">

86(10.76%)

</td>

</tr>

<tr>

<td style="text-align:left;">

E6.5

</td>

<td style="text-align:left;">

276(34.54%)

</td>

</tr>

<tr>

<td style="text-align:left;">

E7.5

</td>

<td style="text-align:left;">

374(46.81%)

</td>

</tr>

</tbody>

</table>

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

Mesoderm

</th>

<th style="text-align:right;">

Primitive\_Streak

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

62

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

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

86

</td>

<td style="text-align:right;">

0

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

187

</td>

<td style="text-align:right;">

39

</td>

<td style="text-align:right;">

49

</td>

</tr>

<tr>

<td style="text-align:left;">

E7.5

</td>

<td style="text-align:right;">

45

</td>

<td style="text-align:right;">

87

</td>

<td style="text-align:right;">

57

</td>

<td style="text-align:right;">

146

</td>

<td style="text-align:right;">

38

</td>

</tr>

</tbody>

</table>

Stage and Lineage seem to be asociated with each other.

## Results

We analyze MOSAIC obtained cross validated solutions over two metrics -
adjusted Mutual Information (AMI) and Standardized Pooled Within Sum of
Squares (SPWSS)

### Stage

<img src="README_figures/README-unnamed-chunk-3-1.png" width="1056" />

  - RNA, Met promoter and Met cgi paltforms track close to each other,
    and are also on top of rest of the platforms in terms of been
    informative towards stage.

  - Integration of all 5 platforms clearly outperforms rest of the
    individual platforms

#### Let’s take a look at RNA MOSAIC solution

<table>

<caption>

MOSAIC rna vs stage, AMI= 0.4

</caption>

<thead>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

E4.5

</th>

<th style="text-align:right;">

E5.5

</th>

<th style="text-align:right;">

E6.5

</th>

<th style="text-align:right;">

E7.5

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

63

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

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

34

</td>

<td style="text-align:right;">

180

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

3

</td>

<td style="text-align:right;">

213

</td>

<td style="text-align:right;">

96

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

83

</td>

<td style="text-align:right;">

29

</td>

<td style="text-align:right;">

63

</td>

</tr>

<tr>

<td style="text-align:left;">

5

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

35

</td>

</tr>

</tbody>

</table>

<table>

<caption>

MOSAIC rna vs lineage, AMI=0.41

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

Mesoderm

</th>

<th style="text-align:right;">

Primitive\_Streak

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

62

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

40

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

162

</td>

<td style="text-align:right;">

11

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

37

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

211

</td>

<td style="text-align:right;">

3

</td>

<td style="text-align:right;">

60

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

8

</td>

<td style="text-align:right;">

13

</td>

<td style="text-align:right;">

119

</td>

<td style="text-align:right;">

20

</td>

<td style="text-align:right;">

15

</td>

</tr>

<tr>

<td style="text-align:left;">

5

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

34

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

</tbody>

</table>

**Let us take a look at some analysis with kmeans**

<table>

<caption>

kmeans rna vs stage, AMI= 0.27

</caption>

<thead>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

E4.5

</th>

<th style="text-align:right;">

E5.5

</th>

<th style="text-align:right;">

E6.5

</th>

<th style="text-align:right;">

E7.5

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

18

</td>

<td style="text-align:right;">

126

</td>

<td style="text-align:right;">

63

</td>

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

116

</td>

<td style="text-align:right;">

48

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

62

</td>

<td style="text-align:right;">

68

</td>

<td style="text-align:right;">

15

</td>

<td style="text-align:right;">

55

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

19

</td>

<td style="text-align:right;">

176

</td>

</tr>

<tr>

<td style="text-align:left;">

5

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

32

</td>

</tr>

</tbody>

</table>

<table>

<caption>

kmeans rna vs lineage, AMI=0.32

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

Mesoderm

</th>

<th style="text-align:right;">

Primitive\_Streak

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

26

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

144

</td>

<td style="text-align:right;">

5

</td>

<td style="text-align:right;">

32

</td>

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

12

</td>

<td style="text-align:right;">

7

</td>

<td style="text-align:right;">

99

</td>

<td style="text-align:right;">

14

</td>

<td style="text-align:right;">

32

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

7

</td>

<td style="text-align:right;">

14

</td>

<td style="text-align:right;">

149

</td>

<td style="text-align:right;">

17

</td>

<td style="text-align:right;">

12

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

34

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

149

</td>

<td style="text-align:right;">

11

</td>

</tr>

<tr>

<td style="text-align:left;">

5

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

32

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

</tr>

</tbody>

</table>

  - We see that supervised approach like MOSAIC leads to a higher AMI
    with stage than kmeans.

Let’s elaborate this via a t-SNE
plot

<img src="README_figures/README-unnamed-chunk-6-1.png" width="768" /><img src="README_figures/README-unnamed-chunk-6-2.png" width="768" />

A slightly better classification via MOSAIC is evident from the tSNE
plot, this is also reflective in their respective AMIs

#### Other MOSAIC solutions

Make a *circomap* of remaining subtypes, and stage and lineage
classification

<img src="README_figures/README-unnamed-chunk-7-1.png" width="768" />

### Integrated solution

<table>

<caption>

integrated vs stage, AMI= 0.68

</caption>

<thead>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

E4.5

</th>

<th style="text-align:right;">

E5.5

</th>

<th style="text-align:right;">

E6.5

</th>

<th style="text-align:right;">

E7.5

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

83

</td>

<td style="text-align:right;">

5

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

62

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

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

2

</td>

<td style="text-align:right;">

258

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

2

</td>

<td style="text-align:right;">

255

</td>

<td style="text-align:right;">

7

</td>

</tr>

<tr>

<td style="text-align:left;">

5

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

14

</td>

<td style="text-align:right;">

109

</td>

</tr>

</tbody>

</table>

<table>

<caption>

integrated vs lineage, AMI=0.22

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

Mesoderm

</th>

<th style="text-align:right;">

Primitive\_Streak

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

87

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

2

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

62

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

26

</td>

<td style="text-align:right;">

64

</td>

<td style="text-align:right;">

37

</td>

<td style="text-align:right;">

102

</td>

<td style="text-align:right;">

31

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

180

</td>

<td style="text-align:right;">

35

</td>

<td style="text-align:right;">

46

</td>

</tr>

<tr>

<td style="text-align:left;">

5

</td>

<td style="text-align:right;">

18

</td>

<td style="text-align:right;">

22

</td>

<td style="text-align:right;">

26

</td>

<td style="text-align:right;">

48

</td>

<td style="text-align:right;">

9

</td>

</tr>

</tbody>

</table>

t-SNE plot of integrated
    solution

    ## Warning in cmdscale(cc, nrow(cc) - 1): only 697 of the first 798 eigenvalues are
    ## > 0

<img src="README_figures/README-unnamed-chunk-9-1.png" width="768" />

Clearly integration makes a huge difference in classifying stage,
showing that information is borrowed across difeerent platforms.

### Met promoter vs RNA

Let’s take a look at the two platforms, RNA and Met promoter that are
most informative for stage.

<table>

<caption>

Met promoter vs stage, AMI=0.45

</caption>

<thead>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

E4.5

</th>

<th style="text-align:right;">

E5.5

</th>

<th style="text-align:right;">

E6.5

</th>

<th style="text-align:right;">

E7.5

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

62

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

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

67

</td>

<td style="text-align:right;">

5

</td>

<td style="text-align:right;">

7

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

70

</td>

<td style="text-align:right;">

236

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

19

</td>

<td style="text-align:right;">

201

</td>

<td style="text-align:right;">

131

</td>

</tr>

</tbody>

</table>

Let’s see how this looks with RNA solution

<table>

<caption>

Met promoter vs RNA, AMI=0.27

</caption>

<thead>

<tr>

<th style="text-align:left;">

</th>

<th style="text-align:right;">

1

</th>

<th style="text-align:right;">

2

</th>

<th style="text-align:right;">

3

</th>

<th style="text-align:right;">

4

</th>

<th style="text-align:right;">

5

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:left;">

1

</td>

<td style="text-align:right;">

62

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

</tr>

<tr>

<td style="text-align:left;">

2

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

6

</td>

<td style="text-align:right;">

5

</td>

<td style="text-align:right;">

68

</td>

<td style="text-align:right;">

0

</td>

</tr>

<tr>

<td style="text-align:left;">

3

</td>

<td style="text-align:right;">

0

</td>

<td style="text-align:right;">

119

</td>

<td style="text-align:right;">

131

</td>

<td style="text-align:right;">

44

</td>

<td style="text-align:right;">

12

</td>

</tr>

<tr>

<td style="text-align:left;">

4

</td>

<td style="text-align:right;">

1

</td>

<td style="text-align:right;">

89

</td>

<td style="text-align:right;">

176

</td>

<td style="text-align:right;">

63

</td>

<td style="text-align:right;">

23

</td>

</tr>

</tbody>

</table>

Interesting to see that even though individual RNA MSOAIC solution (k=5)
and Met promoter (k=4) are both informative towards stage with AMI 0.4
and 0.45 respectively, they are conveying slightly different underlying
information classifying stage. AMI RNA with Met promoter 0.27

Note, that due to missing-ness in Met Promoter data, we didn’t perform
an overlap between common features between RNA and Met Promoter .

## Conclusion

  - MOSAIC finds supervised clusters, with an outcome of interest in
    mind. Where kmeans might give mixed results. Supervised clustering
    is much more efficient and helps in sorting out different signals

  - MOSAIC can run with missing data. However interpretations should be
    made carefully.

  - MOSAIC reduces computation space from sample x feature to sample x
    sample

  - Efficient in dealing with noisy features

## References

1.  Arora A, Olshen AB, Seshan VE, and Shen R. Pan-cancer identification
    of clinically relevant genomic subtypes using outcome-weighted
    integrative clustering. Biorxiv

2.  Xing, E. P., Jordan, M. I., Russell, S. J., & Ng, A. Y. (2003).
    Distance metric learning with application to clustering with
    side-information. In Advances in neural information processing
    systems (pp. 521-528).
