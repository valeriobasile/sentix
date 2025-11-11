# Sentix 3


[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15609215.svg)](https://doi.org/10.5281/zenodo.15609215)
[![License: CC BY
4.0](https://img.shields.io/badge/License-CC%20BY%20SA%204.0-blue.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Sentix is an **affective lexicon for the Italian language**, created in
2013, and available via the `sentixR` R package on GitHub since 2019
(Basile, 2019/2024). Sentix 3 represents a major update, incorporating
an expanded set of lemmas (**70,750 entries** in v3.1), with associated
**polarity scores** (ranging from -1 to +1) and **categorical polarity
classifications** (Positive, Neutral, Negative).

## Background

The original Sentix lexicon was created in 2013 (Basile & Nissim, 2013)
by aligning several lexical resources: *SentiWordNet* (Baccianella et
al., 2010), *MultiWordNet* (Pianta et al., 2002) and *Wordnet*
(Fellbaum, 1998). Performance was evaluated against manually annotated
data.

**Sentix 2.0** aggregated polarity scores for lemma senses into a single
score (-1 to 1) using a weighted average with sense frequencies from the
SemCor corpus (Langone et al., 2004; Vassallo et al., 2020). Sentix 2.0
(41,800 lemmas) has been available via the `sentixR` R package on GitHub
since 2019 (Basile, 2019/2024).

Two derived resources were also developed:

- **MAL (Morphologically-inflected Affective Lexicon)** (Vassallo et
  al., 2019): Expanded Sentix 2.0 with inflected forms from *Morph-it!*
  (Zanchetta & Baroni, 2005) to address lemmatization challenges in
  Italian sentiment analysis.

- **WMAL (Weighted-MAL)** (Vassallo et al., 2020): Recalculated MAL’s
  scores by weighting them with word frequencies from the TWITA corpus
  (Basile & Nissim, 2013) to reduce polarity imbalance. The weighting
  methodology and polarity calculation based on WMAL are key to Sentix
  3.0’s polarity categorical classification.

## Sentix v3.1: Update Process and Features

The main reason for the Sentix 3 update was the decision to harmonize
all three resources (Sentix, MAL, WMAL) to ensure overall consistency.

This overall check involved:

- Identifying entries in Sentix (whether base forms or inflected forms)
  that could generate unexpected duplicate entries when creating MAL.

- Expanding Sentix by back-linking lemmas from *Morph-it!* traceable to
  pre-existing entries.

- Adding neutral terms from SentiWordNet not already present in Sentix
  (29,200 entries, in v3.1).

The resources used include SentiWordNet (Esuli, 2019/2025; see also, for
the Italian synsets, Vardanega, 2025/2025), MultiWordNet via the *Open
Multilingual Wordnet* <https://omwn.org/> (Bond et al., 2023; Bond &
Paik, 2012), the TreeTagger library (Schmid et al., 2007), and
*Morph-it!*.

### Score Calculation

In SentiWordNet the positive $p$ and negative $n$ polarity scores are
assigned to synsets independently, that is, the sum of positive,
negative and neutral score is 1, and no constraint is posed on the
relative size of $p$ and $n$.

Geometrically, a synset can be represented as a point in the cartesian
space, where its *x* coordinate is the positive score and
the *y* coordinate is the negative score.

<img src="https://valeriobasile.github.io/twita/img/sentspace.png"
style="width:50.0%" data-fig-align="center"
alt="Sentiment plane (Basile &amp; Nissim, s.d.)" />  
*The sentiment plane (Basile & Nissim, s.d.)*

Since $x + y ≤ 1$, the *sentiment plane* is restricted to a triangle,
where:

- ***Intensity***, the strength of the sentiment, can be calculated as
  the Euclidean distance of the point $(p, n)$ from the origin:
  $r = \sqrt{p^2 + n^2}$.

- ***Polarity***, the direction of the sentiment (from -1 for negative
  to +1 for positive), can be computed in two steps:

  - First, as the angle $\theta$ that the vector from the origin to
    $(p, n)$ forms with the positive x-axis, which ranges from 0° to
    90°. $\theta = tan^{-1}(\frac{n}{p}) \cdot \frac{180}{\pi}$

  - Then by mapping this angle to -1/+1 (180°).
    $1 - (\frac{4 \cdot \theta}{180})$,

The final score is then computed as *intensity* $\cdot$ *polarity*.

If the same term occurs in multiple synsets, thus having different
sentiment scores, the final score for the lemma is computed as a
weighted average of the scores across its synsets, where the weights are
derived from sense frequencies in the SemCor corpus (Langone et al.,
2004; see Vassallo et al., 2020).

### Polypathy Index

As a measure of quality and reliabiliy of the polarity scores assigned
to lemmas with multiple entries, we introduce the *polypathy index*,
following the proposal by Basile & Nissim (2013).

The column `polypathy_index` provides a qualitative classification
(stored as text) for lemmas based on the variation and ambivalence of
scores across their multiple entries.

The classification is based on the difference between the maximum and
minimum scores (the range). This range is compared against the mean of
this distribution of ranges (0.2717139), calculated across all lemmas
with multiple entries. It also considers whether the scores are
“ambivalent” (i.e., the lemma’s entries include both positive and
negative sentiment scores).

The index is has four levels:”

0: The lemma has no duplicate entries in the lexicon.

1 (Low Variation): The difference between the max and min scores is
below the mean threshold (\< 0.2717139).

2 (High Variation, No Ambivalence): The difference is above the mean
threshold (\> 0.2717139), but all entries share the same polarity
(ambivalence = FALSE).

3 (High Variation, Ambivalent): The difference is above the mean
threshold (\> 0.2717139), and the entries have mixed polarities
(ambivalence = TRUE).

The following table summarizes the polypathy index classification:

| *polypathy index* | range   | ambivalent |      N |
|------------------:|:--------|:-----------|-------:|
|                 0 |         |            | 65.204 |
|                 1 | \< 0.27 | FALSE      |    617 |
|                 2 | \> 0.27 | FALSE      |  2.581 |
|                 3 | \> 0.27 | TRUE       |  2.348 |

## Data Structure and Format

- **File(s):** `sentix_v3.1.csv`
- **Encoding:** UTF-8
- **Separator:** Comma (`,`)
- **Columns:**
  - `lemma`: (string) The lemma.
  - `score`: (float) The polarity score (-1, 1).
  - `polarity`: (string) The polarity classification (“Positive”,
    “Negative”, “Neutral”).
  - `polypathy_index`: (string) The polypathy index (classification
    levels 0, 1, 2, 3).

## License

This dataset is released under the [Creative Commons Attribution 4.0
International (CC BY SA 4.0)
License](https://creativecommons.org/licenses/by-sa/4.0/).

## How to Cite Sentix 3

If you use Sentix 3 in your research, please cite it as follows:

Basile, V., Nissim, M., Bosco, C., Vassallo, M., & Gabrieli, G. (2025).
Sentix (Versione 3.1.0) \[Dataset\].
https://doi.org/10.5281/zenodo.15609185

## Authors

**Creators:**

- Basile, Valerio (Università di Torino)

- Nissim, Malvina (Università di Groningen)

- Bosco, Cristina (Università di Torino)

- Gabrieli, Giuliano (CREA-PB)

- Vassallo, Marco (CREA-PB)

**Contributors:**

- Vardanega, Agnese (Università di Teramo)

## References

<div id="refs" class="references csl-bib-body hanging-indent"
entry-spacing="0" line-spacing="2">

<div id="ref-baccianella2010" class="csl-entry">

Baccianella, S., Esuli, A., & Sebastiani, F. (2010). *Sentiwordnet 3.0:
An enhanced lexical resource for sentiment analysis and opinion mining.*
*10*, 22002204.
<http://lrec-conf.org/proceedings/lrec2010/pdf/769_Paper.pdf>

</div>

<div id="ref-basile2024" class="csl-entry">

Basile, V. (2024). *Valeriobasile/<span class="nocase">sentixR</span>*
\[Computer software\]. <https://github.com/valeriobasile/sentixR>
(Original work published 2019)

</div>

<div id="ref-basile_sentiment_" class="csl-entry">

Basile, V., & Nissim, M. (n.d.). *Sentiment Analysis*. Twita. Retrieved
January 6, 2025, from
<https://valeriobasile.github.io/twita/sentix.html>

</div>

<div id="ref-basile2013" class="csl-entry">

Basile, V., & Nissim, M. (2013). *Sentiment analysis on italian tweets*.
100107. <https://aclanthology.org/W13-1614/>

</div>

<div id="ref-bond_documenting_2023" class="csl-entry">

Bond, F., Goodman, M. W., Rudnicka, E., da Costa, L. M., Rademaker, A.,
& McCrae, J. P. (2023). Documenting the Open Multilingual Wordnet. In G.
Rigau, F. Bond, & A. Rademaker (Eds.), *Proceedings of the 12th Global
Wordnet Conference* (pp. 150–157). Global Wordnet Association.

</div>

<div id="ref-bond2012" class="csl-entry">

Bond, F., & Paik, K. (2012). *A survey of wordnets and their licenses*.
6471. <https://www.academia.edu/download/31907561/gwc2012.pdf#page=69>

</div>

<div id="ref-esuli_aesuli_2025" class="csl-entry">

Esuli, A. (2025). *SentiWordNet* \[Computer software\].
<https://github.com/aesuli/SentiWordNet> (Original work published 2019)

</div>

<div id="ref-fellbaum1998" class="csl-entry">

Fellbaum, C. (1998). *Towards a representation of idioms in WordNet*.
<https://aclanthology.org/W98-0707.pdf>

</div>

<div id="ref-langone2004" class="csl-entry">

Langone, H., Haskell, B. R., & Miller, G. A. (2004). Annotating WordNet.
*Proceedings of the Workshop Frontiers in Corpus Annotation at HLT-NAACL
2004*, 63–69.

</div>

<div id="ref-pianta2002" class="csl-entry">

Pianta, E., Bentivogli, L., & Girardi, C. (2002). *MultiWordNet:
Developing an aligned multilingual database*. 293302.
<https://cris.fbk.eu/handle/11582/499>

</div>

<div id="ref-schmid2007" class="csl-entry">

Schmid, H., Baroni, M., Zanchetta, E., & Stein, A. (2007). Il sistema
‘tree-tagger arricchito’the enriched TreeTagger system. *IA Contributi
Scientifici*, *4*(2), 2223.
<https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=05eb28ad2dc51c9a00cb6f4bbd953db7a81e14fc>

</div>

<div id="ref-vardanega_sentiwordnet_it_2025" class="csl-entry">

Vardanega, A. (2025). *Sentiwordnet_it* \[Dataset\].
<https://github.com/agnesevardanega/sentiwordnet_it> (Original work
published 2025)

</div>

<div id="ref-vassallo2019" class="csl-entry">

Vassallo, M., Gabrieli, G., Basile, V., & Bosco, C. (2019). *The
tenuousness of lemmatization in lexicon-based sentiment analysis*.
*2481*, 16. <https://iris.unito.it/bitstream/2318/1725233/1/paper74.pdf>

</div>

<div id="ref-vassallo2020" class="csl-entry">

Vassallo, M., Gabrieli, G., Basile, V., & Bosco, C. (2020). *Polarity
imbalance in lexicon-based sentiment analysis*. 17.
<https://iris.unito.it/bitstream/2318/1764610/1/paper_36.pdf>

</div>

<div id="ref-zanchetta2005" class="csl-entry">

Zanchetta, E., & Baroni, M. (2005). *Morph-it! A free corpus-based
morphological resource for the italian language*. *1*, 112.
<https://cris.unibo.it/handle/11585/15321>

</div>

</div>
