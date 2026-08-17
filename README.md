# Kyoto Pediatric Care Locations: Mixed-Methods Review Analysis

This repository provides the cleaned dataset, quantitative analysis code, and qualitative analysis materials accompanying the study:

> **A Mixed-Methods Analysis of Online Reviews of Pediatric Care: A Case Study in Kyoto, Japan**

The study analyzes Google Maps reviews of healthcare locations providing pediatric care in Kyoto, Japan, using a mixed-methods design that combines multi-model sentiment analysis with qualitative thematic analysis in MAXQDA.

## Overview

The dataset contains **4,086 Google Maps reviews from 110 pediatric-care locations in Kyoto, Japan**. Of these, **3,981 reviews contain usable text** and are included in the text-based analyses.

The study investigates three main questions:

1. How strongly are Google star ratings associated with independently inferred textual sentiment?
2. How robust are rating–sentiment patterns across different sentiment models, and where does model disagreement concentrate?
3. What qualitative experience themes characterize positive, intermediate, and negative rating strata, and how do these themes help explain rating–text convergence and ambiguity?

The repository is provided to improve the **transparency and reproducibility** of both the quantitative and qualitative analyses.

---

## Repository Contents

### Data

- `Kyoto_clinics.xlsx`  
  Original consolidated review dataset used in the project.

- `Kyoto_clinics_GPT56Sol_final.xlsx`  
  Cleaned and processed dataset containing review identifiers, ratings, review text, location information, and derived analysis fields used in the quantitative workflow.

### Quantitative Analysis

- `01_prepare_batch_Kyoto_Clinics_GPT56_Sol*.ipynb`  
  Prepares review text and related inputs for GPT-5.6 Sol sentiment inference.

- `02_analyze_Kyoto_Clinics_Mixed_Methods*.ipynb`  
  Performs the main quantitative analysis and generates statistics and visualizations used in the paper.

The quantitative analysis compares five text-only sentiment systems:

- GPT-5.6 Sol
- CardiffNLP RoBERTa
- BERTweet
- Qwen3.5-9B
- Gemma 3 12B IT

Star ratings are **not treated as sentiment ground-truth labels**. Instead, the analysis examines rating–sentiment association, cross-model agreement, model consensus, and model-vote entropy.

### Qualitative Analysis

The MAXQDA projects contain the reviewed and consolidated qualitative coding for the three rating strata:

- `positives.mqda` — positive reviews (4–5 stars)
- `neutrals.mqda` — intermediate / three-star reviews
- `negatives.mqda` — negative reviews (1–2 stars)

The three strata are intentionally maintained as **separate qualitative codebooks** because they address different analytical questions:

- 4–5 stars: factors associated with favorable reviewer experiences
- 3 stars: mixed and qualified experiences
- 1–2 stars: factors associated with unfavorable reviewer experiences

Higher-level thematic domains are subsequently compared across strata for mixed-methods interpretation.

---

## Data Collection and Preprocessing

Google Maps reviews were collected on **18 July 2026** from **110 selected healthcare locations providing pediatric care in Kyoto Prefecture, Japan**.

The processing workflow included:

- merging reviews from the selected locations;
- standardizing fields and location identifiers;
- auditing duplicate and missing-text records;
- parsing relative Google review dates;
- estimating review year where possible;
- assigning unique review IDs and anonymized location codes; and
- creating the final text-analysis subset.

The complete dataset contains:

| Item | Count |
|---|---:|
| Review records | 4,086 |
| Reviews with usable text | 3,981 |
| Reviews without text | 105 |
| Pediatric-care locations | 110 |

Displayed Google Maps review dates extend approximately from **2012 to 2026**. Because Google Maps may display relative dates and identify some reviews as edited, estimated review years should not be interpreted as exact original publication dates.

---

## Quantitative Analysis

Sentiment is represented using three classes:

- Negative = -1
- Neutral = 0
- Positive = +1

The main quantitative analyses include:

- sentiment distribution by star rating;
- Spearman rank correlation between rating and textual sentiment;
- pairwise raw model agreement;
- pairwise Cohen's kappa;
- five-model Fleiss' kappa;
- model consensus strength;
- normalized model-vote entropy;
- review-length analysis; and
- location-level rating–text heterogeneity.

No individual sentiment model is treated as ground truth.

---

## Qualitative Analysis

The qualitative analysis was conducted using **MAXQDA Analytics Pro**.

Reviews were organized into three rating strata:

- **Positive:** 4–5 stars
- **Intermediate:** 3 stars
- **Negative:** 1–2 stars

Before detailed coding, vague or non-informative reviews were excluded from the qualitative coding subsets.

Retained qualitative subsets:

| Rating stratum | Retained reviews |
|---|---:|
| Positive (4–5 stars) | 1,333 |
| Intermediate (3 stars) | 212 |
| Negative (1–2 stars) | 1,483 |

Each retained review can receive multiple qualitative codes. Therefore, code-application frequencies can exceed the number of reviews.

Initial codes were reviewed against the source text, semantically overlapping codes were consolidated, and related codes were organized into higher-level thematic domains.

Sentiment-model predictions and cross-model agreement measures were **not used to assign the qualitative codes**.

---

## Key Findings

The quantitative results show a strong ordinal relationship between Google star ratings and independently inferred textual sentiment.

Across the five sentiment models:

- Spearman correlations range from approximately **0.811 to 0.890**;
- pairwise raw agreement ranges from **83.1% to 94.9%**;
- pairwise Cohen's kappa ranges from **0.719 to 0.909**; and
- five-model Fleiss' kappa is **0.789**.

Model disagreement is concentrated in intermediate ratings. In particular, **51.1% of three-star reviews are non-unanimous across the five models**, substantially higher than one-star or five-star reviews.

The qualitative analysis helps explain this pattern:

- high-rating reviews emphasize kindness, professionalism, reassurance, clinical competence, communication, child- and family-centered care, and accessibility;
- three-star reviews frequently combine favorable and unfavorable experience dimensions; and
- low-rating reviews emphasize interpersonal disrespect, waiting and access problems, clinical and safety concerns, administrative difficulties, and service inconsistency.

The combined results suggest that intermediate ratings should not automatically be interpreted as neutral sentiment.

---

## Reproducibility

The repository is intended to support reproduction and inspection of the analyses reported in the accompanying paper.

A typical workflow is:

1. Inspect the cleaned dataset.
2. Run the preparation notebook for model inference.
3. Run the quantitative analysis notebook.
4. Open the three `.mqda` projects in MAXQDA to inspect qualitative coding.
5. Compare the resulting quantitative and qualitative findings using the mixed-methods framework described in the paper.

Exact reproduction of proprietary model outputs may depend on model availability, software versions, API configuration, and inference settings.

---

## Important Interpretation Notes

The reviews are interpreted as **reviewer-reported pediatric-care experiences**.

Reviewer identity and relationship to the child are unknown. A reviewer may be a patient, parent, guardian, family member, or another accompanying person. The dataset therefore should **not** be interpreted as a collection of direct patient-reported outcomes.

Google Maps reviewers are also self-selected, so the results should not be interpreted as representative estimates of the clinical quality of individual healthcare locations.

Location-level analyses are used for descriptive heterogeneity analysis and are **not quality rankings**.

---

## Data and Ethical Considerations

The source material consists of publicly accessible online reviews. Users of this repository should nevertheless handle review text responsibly and avoid attempting to identify individual reviewers.

The dataset is provided for research and reproducibility purposes. Users are responsible for ensuring that their use of the data complies with applicable platform terms, institutional requirements, and ethical standards.

---

## Software

The analyses use tools including:

- Python
- Jupyter Notebook
- pandas
- NumPy
- SciPy
- scikit-learn
- Matplotlib
- Hugging Face Transformers
- MAXQDA Analytics Pro

Additional package requirements can be identified from the corresponding notebooks.

---

## Citation

If you use this dataset, code, or qualitative analysis materials, please cite the accompanying paper:

> Walalawela Kaveesha Kavindi, Tai Dinh, and Wuyi Yue.  
> **A Mixed-Methods Analysis of Online Reviews of Pediatric Care: A Case Study in Kyoto, Japan.**  
> Submitted to MEDI 2026.

Bibliographic information will be updated after publication.

---

## Authors

**Walalawela Kaveesha Kavindi**  
The Kyoto College of Graduate Studies for Informatics, Kyoto, Japan

**Tai Dinh**  
The Kyoto College of Graduate Studies for Informatics, Kyoto, Japan  
ORCID: 0000-0001-7597-4262  
Email: t_dinh@kcg.ac.jp

**Wuyi Yue**  
The Kyoto College of Graduate Studies for Informatics, Kyoto, Japan

---

## Repository

**Kyoto Pediatric Care Locations**  
https://github.com/taiduydinh/kyoto-pediatric-care-locations
