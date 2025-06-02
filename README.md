# Sentix v3.0

[![DOI](https://zenodo.org/badge/DOI/YOUR_ZENODO_DOI.svg)](https://doi.org/YOUR_ZENODO_DOI) [![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)



Sentix is an **affective lexicon for the Italian language**, created in 2013 by aligning several lexical resources. This version, Sentix 3.0, represents a significant update, incorporating an expanded set of lemmas (**63,660 entries**), with associated **affective scores** (ranging from -1 to +1) and categorical **polarity classifications** (Positive, Neutral, Negative).

## Background

The original Sentix lexicon was created in 2013 by aligning several lexical resources: SentiWordNet (Baccianella et al., 2010), MultiWordNet (Pianta et al., 2002), Wordnet (Fellbaum, 1998a, 1998b), and BabelNet (Navigli & Ponzetto, 2010, 2012).

- **Sentix 1.0** (Basile & Nissim, 2013): Built by transferring SentiWordNet *synset* annotations to Italian *synsets* from MultiWordNet. Performance was evaluated against manually annotated data.

- **Sentix 2.0**: Aggregated polarity scores for lemma senses into a single score (-1 to 1) using a weighted average with sense frequencies from the SemCor corpus (Langone et al., 2004; Vassallo et al., 2020). Sentix 2.0 (41,800 lemmas) has been available via the `sentixR` R package on GitHub since 2019 (Basile, 2024).

Several derived resources were also developed:

- **MAL (Morphologically-inflected Affective Lexicon)** (Vassallo et al., 2019): Expanded Sentix 2.0 with inflected forms from *Morph-it!* (Zanchetta & Baroni, 2005) to address lemmatization challenges in Italian sentiment analysis.

- **WMAL (Weighted-MAL)** (Vassallo et al., 2020): Recalculated MAL’s scores by weighting them with word frequencies from the TWITA corpus (Basile & Nissim, 2013) to reduce polarity imbalance. The weighting methodology and polarity calculation based on WMAL are key to Sentix 3.0’s polarity assignments.

## Sentix v3.0: Update Process and Features

The update leading to Sentix 3.0 was the decision to harmonize all three resources (Sentix, MAL, WMAL) to ensure overall consistency.

This overall check involved:
* Identifying entries in Sentix (i.e., entries that could be either base forms or inflected forms) that could generate unexpected duplicate entries when creating MAL.
* Expanding Sentix by back-linking lemmas from *Morph-it!* traceable to pre-existing entries.
* Adding neutral terms from SentiWordNet not already present in Sentix (22,117 entries).

The resources used for this update include SentiWordNet, MultiWordNet (via *Open Multilingual Wordnet* <https://omwn.org/> (Bond et al., 2023; Bond & Paik, 2012), the TreeTagger library (Schmid et al., 2007), and *Morph-it!*.

## Data Structure and Format

* **File(s):** `sentix_v3.0.csv`
* **Encoding:** UTF-8
* **Separator:** Comma (`,`)
* **Columns:**
    * `lemma`: (string) The lemma.
    * `score`: (float) The polarity score (-1, 1).
    * `polarity`: (string) "Positive", "Negative", "Neutral".


## License

This dataset is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0) License](https://creativecommons.org/licenses/by/4.0/).

## How to Cite Sentix v3.0

If you use Sentix v3.0 in your research, please cite it as follows:

(Autori di Sentix v3.0). (Anno di Pubblicazione su Zenodo). *Sentix v3.0*. Zenodo. https://doi.org/YOUR_ZENODO_DOI_ONCE_AVAILABLE


## Authors 

**Creators (Sentix v3.0):**
* Basile, Valerio (Università di Torino, ORCID: 0000-0001-8110-6832)
* Nissim, Malvina (Università di Pisa, ORCID: 0000-0001-5289-0971)
* Vassallo, Marco (CREA-PB, ORCID: 0000-0001-7016-6549)
* Gabrieli, Giuliano (CREA-PB, ORCID: 0009-0005-1153-5662)

**Contributors (Sentix v3.0):**
* Vardanega, Agnese (Università di Teramo, ORCID: 0000-0002-1419-9896, Role: DataCurator)

## Contact

For any questions regarding this dataset, please contact:
[nome e email di contatto, o un link a un issue tracker su GitHub]


## References (from the text, for context)

Baccianella, S., Esuli, A., & Sebastiani, F. (2010). Sentiwordnet 3.0: An enhanced lexical resource for sentiment analysis and opinion mining. *Lrec*, *10*, 2200–2204.

Basile, V. (2024). *Valeriobasile/sentixR*.

Basile, V., & Nissim, M. (2013). Sentiment analysis on Italian tweets. *Proceedings of the 4th Workshop on Computational Approaches to Subjectivity, Sentiment and Social Media Analysis*, 100–107.

Bond, F., Goodman, M. W., Rudnicka, E., da Costa, L. M., Rademaker, A., & McCrae, J. P. (2023). Documenting the Open Multilingual Wordnet. In G. Rigau, F. Bond, & A. Rademaker (Eds.), *Proceedings of the 12th Global Wordnet Conference* (pp. 150–157). Global Wordnet Association.

Bond, F., & Paik, K. (2012). A survey of wordnets and their licenses. *Proceedings of the 6th Global WordNet Conference (GWC 2012)*, 64–71.

Fellbaum, C. (1998a). Towards a representation of idioms in WordNet. *Usage of WordNet in Natural Language Processing Systems*.

Fellbaum, C. (1998b). *WordNet: An electronic lexical database*. MIT press.

Langone, H., Haskell, B. R., & Miller, G. A. (2004). Annotating WordNet. *Proceedings of the Workshop Frontiers in Corpus Annotation at HLT-NAACL 2004*, 63–69.

Navigli, R., & Ponzetto, S. P. (2010). BabelNet: Building a very large multilingual semantic network. *Proceedings of the 48th Annual Meeting of the Association for Computational Linguistics*, 216–225.

Navigli, R., & Ponzetto, S. P. (2012). BabelNet: The automatic construction, evaluation and application of a wide-coverage multilingual semantic network. *Artificial Intelligence*, *193*, 217–250.

Pianta, E., Bentivogli, L., & Girardi, C. (2002). MultiWordNet: Developing an aligned multilingual database. *First International Conference on Global WordNet*, 293–302.

Schmid, H., Baroni, M., Zanchetta, E., & Stein, A. (2007). Il sistema “tree-tagger arricchito”–The enriched TreeTagger system. *IA Contributi Scientifici*, *4*(2), 22–23.

Vassallo, M., Gabrieli, G., Basile, V., & Bosco, C. (2019). The tenuousness of lemmatization in lexicon-based sentiment analysis. *Proceedings of the Sixth Italian Conference on Computational Linguistics*, *2481*, 1–6.

Vassallo, M., Gabrieli, G., Basile, V., & Bosco, C. (2020). Polarity Imbalance in Lexicon-based Sentiment Analysis. In F. Dell’Orletta, J. Monti, & F. Tamburini (Eds.), *Proceedings of the Seventh Italian Conference on Computational Linguistics CLiC-it 2020 : Bologna, Italy, March 1-3, 2021* (pp. 457–463). Accademia University Press. <https://doi.org/10.4000/books.aaccademia.8964>

Zanchetta, E., & Baroni, M. (2005). Morph-it! A free corpus-based morphological resource for the Italian language. *Proceedings of Corpus Linguistics Conference Series 2005 (ISSN 1747-9398)*, *1*, 1–12.


