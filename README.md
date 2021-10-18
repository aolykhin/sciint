# Scientific Integrity Dataset
### Version 8, last revision time: July 21, 2021

This repository presents the Scientific Integrity Dataset designed to benchmark semi-automated scientific integrity analytics.

*All collected data are public available and were collected from scientific publishers or trustworthy repositories (e.g., [PubMed](https://pubmed.ncbi.nlm.nih.gov/)).*



## Dataset

The dataset contains detailed information of **988** scientific papers concentrated in the Biomedical area.

During the collection of the articles, we started selecting articles that had been retracted due to image problems.

After this, we expanded the dataset to include others articles that were published by the same authors from the initial set.

At this point, the dataset had **656** papers of which **545** were retracted/corrected -- we organized the retraction/correction reasons by categories in this [Table](#retraction-reasons).

In addition to these data, we also included **332** papers with no retraction/correction selected from the [PMC Open Access Subset](https://www.ncbi.nlm.nih.gov/pmc/tools/openftlist/) to test possibles false alarms from the system, totalizing 988 (656 + 332) articles.

*Disclaimer: Inclusion in the dataset does not necessarily signify that an article is the subject of any research misconduct practice, allegation, or proceeding.*



### Dataset Task Modalities

The dataset contain annotations for five task that assist the process of a scientific integrity document analysis.


| Task                                 | Annotation                                                   | #Articles | #Figures |
| :----------------------------------- | :----------------------------------------------------------- | :-------- | :------- |
| [PDF Content Extraction](https://github.com/danielmoreira/sciint/tree/pdf-content-extraction/pdf-content-extraction-data)               | **Position of each figure within the PDF** document along with the position of its caption.  It also contains the *figures and captions* associated with the online version of the article. | 285       | 1876     |
| [Scientific Figure Panel Segmentation](https://github.com/danielmoreira/sciint/tree/content-segmentation/panel-segmentation-data) | **Position of each panel of a multi-panel scientific figure**. | 48        | 303      |
| [Image Ranking](https://github.com/danielmoreira/sciint/tree/content-ranking/ranking_data)                        | **Content Image-Base Retrieval annotation for scientific images** -- only single-panel figures were included in the annotation. | 48        | 2843     |
| [Copy-Move Detection](https://github.com/danielmoreira/sciint/tree/copy-move-detection/copy-move-data)                  | **Scientific Image Copy-Move Forgery Detection annotation at pixel-wise level** based on retraction notices' description. | 125       | 180      |
| [Provenance Analysis](https://github.com/danielmoreira/sciint/tree/provenance-analysis/provenance_data)                  | **Provenance graph annotations of scientific figures with reused and manipulated regions.** | 85        | 591      |



The dataset is public released in two formats: 

- [Spreadsheet](#csv-file) -- CSV
- [Document-based](#json-file)  -- JSON

Both files contain the URLs that allows a user to download all PDFs and Figures related to each article in the dataset.

If you want to have access to our copy of the PDFs and Figures related to each article in the dataset _for academic research purposes_, please contact [Daniel Moreira](https://github.com/danielmoreira/sciint/blob/provenance-analysis/daniel.moreira@nd.edu).

## <a name="csv-file">SPREADSHEET</a>

The [Spreadsheet](scientific-integrity-dataset.csv)  is designed to be used by non-experts in computer science and as a quick reference to the *Scientific Integrity Dataset* 

<details>
<summary>Spreadsheet Structure - click to expand</summary><p>


| Spreadsheet Column             | Explanation                                                  |
| :----------------------------- | :----------------------------------------------------------- |
| DOI                            | Digital Object Identifier or Pubmed ID (if DOI does not exist) |
| Link                           | Article URL                                                  |
| Creative Commons               | ( Is the article licensed under Creative Commons ? ) Yes / No |
| Retracted/Corrected            | ( Is the article Retracted/Corrected? ) Yes / No             |
| Retraction/Correction DOI      | Retraction/Correction DOI (when applicable)                  |
| Retraction/Correction Reason   | List of Retraction/Correction Reasons (when applicable)<br />Check [Table of  Retraction/Correction Reasons](retraction-reasons) |
| False Alarm Test               | ( Was the article selected to test false alarms?) Yes / No |
| Content Extraction Annotation  | ( Does the article have Content Extraction Annotation ? ) Yes / No |
| Image Ranking Annotation       | ( Does the article have Image Ranking Annotation ? ) Yes / No |
| Panel Segmentation Annotation  | ( Does the article have Panel Segmentation Annotation ? ) Yes / No |
| Copy-Move Detection Annotation | ( Does the article have Copy-Move Annotation ? ) Yes / No    |
| Provenance Analysis Annotation | ( Does the article have Provenance Analysis Annotation ? ) Yes / No |

</p>
</details>

## <a name="json-file">Document-Based Annotation</a>

The [Document-based annotation](scientific-integrity-dataset.json) is a JSON-based document with detailed information of each article included in the Scientific Integrity Dataset.

If you are not a computer science expert, we recommend using a [JSON viewer](http://jsonviewer.stack.hu/) to analyze these annotations.

<details>
<summary>Article JSON Structure - click to expand</summary><p>

```python
						     ############################################################################################
						     ###                                 Field Explanation                                    ###
                                                     ############################################################################################
	
	
< article_id >: {                                    # Article ID is its DOI or PMID (case that DOI does not exist)
    'abstract': < content > ,                        # Article's Abstract
    'access_type': < content > ,	             # FREE or PURSHED
	
    'article_history': {			     # History of Article from submission to acception
        'accepted_date': < yyyy - mm - dd > ,        
        'published_date': < yyyy - mm - dd > ,       
        'received_date': < yyyy - mm - dd >          
    },
    'article_url': < content > ,                     # URL of the online article's version if available; otherwise, article's PubMed Central URL
    'authors': < list - of -authors > ,              # Name of the authors with their affiliation
    'cited_by': < content > ,                        # Number of citation received as of July 21, 2021
    'copyright': < content > ,                       # Aticle's copyright
    'doi': < content > ,                             # Digital Object Identifier

    'figures': {				     # Figure from the Article found on trustworthy sources (Publisher or PMC)
        'fig1': {				     # Figure element
            'fig-caption': < content > ,             # Figure caption collected from the trustworthy source
            'fig-label': < content > ,		     # Figure label (e.g. Fig. 1)
            'fig-link': < content >                  # Figure's URL from the trustworthy source
        },
    },

    'keywords': < list - of -keywords > ,           # List of Article keywords
    'pdf_link': < content > ,                       # Article's PDF URL
    'publication_source': < content > ,             # Name of the article's Journal
    'publisher': < content > ,                      # Name of the article's Publisher
    'supplementary_material_links': < list - of -links > ,  # Links to all article's supplementary material
    'title': < content > ,                          # Article's title

    # Retracted/Corrected articles (as of July 21, 2021) will have the following field
    'retraction_correction_material': {             # All retraction/correction material found
        'retraction_correction_doi': < content > ,  # Retraction/Correction DOI
        'retraction_correction_figures': < list - of -dict > , # All new figures related to the Retraction/Correction Notice
        'retraction_correction_notice_pdf_link': < content > , # Retraction/Correction PDF URL
        'retraction_correction_notice_txt': < content > ,      # Full Text of the Retraction/Correction
        'retraction_correction_reason': < list - of -reasons > # List of reasons to retract/correct the article
    },
}
```

</p>
</details>

## <a name="retraction-reasons"> Table of Retraction/Correction Reasons</a>

| Retraction/Correction Reason      | Explanation                                                  |
| :-------------------------------- | :----------------------------------------------------------- |
| Article Duplication               | Article contains near-duplicated images, text, and data from previous publications. |
| Text Duplication                  | Article contains near-duplicated text from previous publications. |
| Data Duplication                  | Article contains near-duplicated data from previous publications. |
| Image Duplication Across Articles | Article contains near-duplicated images from previous publications. |
| Image Duplication                 | Article contains a duplicated image within itself (e.g., a western-blot panel appears duplicated in the same figure or in two figure from the *same* article). |
| Duplicated Video                  | Article contains a duplicated video within itself.           |
| Data Error                        | Data presented in the article contains errors. (e.g., calculation error, data contamination). |
| Text Error                        | Article contains text typos that were corrected with a *Correction Notice* |
| Graph Error                       | Plots/chars present an error (e.g., use of an old version of the dataset to plot the data). |
| Image Error                       | The image contains a presentation error (e.g., an image was mislabeled). |
| Image Falsification/Fabrication   | Image contains evidences of Falsification or Fabrication.    |
| Image Manipulation                | Image contains evidences of manipulation (e.g., the background of a microscopy photo was erased). |
| Invalid References                | Article contains invalid references.                         |
| No Information                    | The *Retraction/Correction Notice* does not present any information regarding the retraction/correction. |
| Data Falsification/Fabrication    | Data contains evidences of Falsification or Fabrication. |
| Questionable Data                 | The authors were unable to prove the integrity of some data from the article |
| Questionable Image                | The authors were unable to prove the integrity of at least an image from the article. |
| Unreproducible Experiments        | Article contains unreproducible experiments.                 |
| Wrong Author Information          | Article contains wrong author information (e.g., typo in author's name)      |
