# Sentix v3.0: An Affective Lexicon for Italian

[![DOI](https://zenodo.org/badge/DOI/YOUR_ZENODO_DOI.svg)](https://doi.org/YOUR_ZENODO_DOI) [![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)



Sentix is a polarity lexicon for the Italian language, created in 2013 by aligning several lexical resources. This version, Sentix 3.0, represents a significant update, incorporating an expanded set of lemmas and polarity assignments.

This version, Sentix 3.0, contains **63,660 lemmas**, with associated **affective scores** (ranging from -1 to +1) and categorical **polarity classifications** (Positive, Neutral, Negative).

## Background

The original Sentix lexicon was created in 2013 by aligning several lexical resources: SentiWordNet [@baccianella_sentiwordnet_2010], MultiWordNet [@pianta_multiwordnet_2002], Wordnet [@fellbaum_representation_1998; @fellbaum_wordnet_1998], and BabelNet [@navigli_babelnet_2010; @navigli_babelnet_2012].

* **Sentix 1.0** [@basile_sentiment_2013]: Built by transferring SentiWordNet *synset* annotations to Italian *synsets* from MultiWordNet. Performance was evaluated against manually annotated data.
* **Sentix 2.0**: Aggregated polarity scores for lemma senses into a single score (-1 to 1) using a weighted average with sense frequencies from the SemCor corpus [@langone_annotating_2004; @vassallo_polarity_2020]. Sentix 2.0 (41,800 lemmas) has been available via the `sentixR` R package on GitHub since 2019 [@basile_valeriobasile_2024].

Several derived resources were also developed:
* **MAL (Morphologically-inflected Affective Lexicon)** [@vassallo_tenuousness_2019]: Expanded Sentix 2.0 with inflected forms from *Morph-it!* [@zanchetta_morphit_2005] to address lemmatization challenges in Italian sentiment analysis, especially for social media content.
* **WMAL (Weighted-MAL)** [@vassallo_polarity_2020]: Recalculated MAL's scores by weighting them with word frequencies from the TWITA corpus [@basile_sentiment_2013] to reduce polarity imbalance. The weighting methodology and polarity calculation based on WMAL are key to Sentix 3.0's polarity assignments. 

## Sentix v3.0: Update Process and Features

The update leading to Sentix 3.0 was the decision to harmonize all three resources (Sentix, MAL, WMAL) to ensure overall consistency.

This overall check involved:
* Identifying entries in Sentix (i.e., entries that could be either base forms or inflected forms) that could generate unexpected duplicate entries when creating MAL.
* Expanding Sentix by back-linking lemmas from *Morph-it!* traceable to pre-existing entries.
* Adding neutral terms from SentiWordNet not already present in Sentix (22,117 entries).

The resources used for this update include SentiWordNet, MultiWordNet (via *Open Multilingual Wordnet* <https://omwn.org/> [@bond_documenting_2023; @bond_survey_2012]), the TreeTagger library [@schmid_sistema_2007], and *Morph-it!*.

## Data Structure and Format

* **File(s):** `sentix_v3.0.csv`
* **Encoding:** UTF-8
* **Separator:** Comma (`,`)
* **Columns:**
    * `lemma`: (string) The lemma.
    * `score`: (float) The polarity score (e.g., ranging from -1 to 1). Explain how it's derived or interpreted.
    * `polarity`: (string) Categorical polarity (e.g., "Positive", "Negative", "Neutral").


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

*Note: These are references cited in the description above. The full bibliography related to the development and use of Sentix can be found in associated publications.*

* [@baccianella_sentiwordnet_2010] S. Baccianella, A. Esuli, F. Sebastiani, Sentiwordnet 3.0: An enhanced lexical resource for sentiment analysis and opinion mining., in: Lrec, volume 10, Valletta, 2010, pp. 2200-2204.
* [@pianta_multiwordnet_2002] E. Pianta, L. Bentivogli, C. Girardi, MultiWordNet: Developing an aligned multilingual database, in: First International Conference on Global WordNet, 2002, pp. 293-302.
* ... (elenca le altre citazioni Pandoc usate nel testo del README se vuoi espanderle qui, o fai riferimento al tuo `.bib` principale. Per un README, spesso non si espandono tutte le citazioni in una bibliografia completa, ma si rimanda al paper).


