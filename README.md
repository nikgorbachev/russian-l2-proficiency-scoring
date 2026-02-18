# Automated Essay Scoring for Russian as a Second Language: A Deep Ordinal Learning Approach

[![Read the Thesis](https://img.shields.io/badge/📖-Read_the_Thesis-blue?style=for-the-badge)](./docs/Gorbachev_Nikolai_2026_Russian_AES_Thesis.pdf)

**Master's Thesis in Digital Humanities and Digital Knowledge**  
**University of Bologna (UNIBO)**  

**Author:** Nikolai Gorbachev  
**Supervisor:** Prof. Fabio Tamburini  
**Co-Supervisor:** Prof. Mikhail Kopotev (University of Helsinki)


---

## Abstract

Automated Essay Scoring (AES) systems are critical for scaling language assessment, yet most research focuses on English and large-scale datasets. This thesis addresses the challenge of developing reliable AES models for Russian as a Second Language (L2), a morphologically rich language, within the resource-constrained context of institutional learning. The study utilizes a real-world dataset of approximately 1,100 learner essays from the Russian language course at the Middlebury Language School (VT, USA), rated according to the ACTFL proficiency guidelines.

The research systematically evaluates three modeling paradigms: (1) feature-based statistical models relying on engineered linguistic metrics (e.g., syntactic complexity, lexical diversity); (2) deep representation learning using fine-tuned multilingual Transformers (XLM-RoBERTa); and (3) hybrid fusion strategies. A central innovation of this work is the application of **Ordinal Regression objectives**, specifically **Consistent Rank Logits (CORAL)** and **Conditional Ordinal Regression (CORN)**, to explicitly model the ordered nature of proficiency levels.

Results demonstrate that the Deep Ordinal approach (**XLM-RoBERTa + CORAL**) achieves competitive performance under low-resource conditions, substantially outperforming feature-based baselines and standard cross-entropy models.


## Key Contributions

- First application of CORAL and CORN ordinal objectives to Russian L2 AES.
- Empirical comparison of feature-based, transformer-based, and fusion paradigms.
- Analysis of linguistic feature evolution across ordinal proficiency thresholds.
- Demonstration that ordinal objectives improve rank consistency over cross-entropy.





## Repository Structure

This repository is organized as a sequential research pipeline, corresponding to the chapters of the thesis.

```text
.
├── data/                       # (Excluded from repo for privacy) Dataset placeholders
├── docs/
│   ├── Gorbachev_Nikolai_2026_Russian_AES_Thesis.pdf  # Full Thesis Text
├── notebooks/                  # Experimental pipeline
│   ├── 01_preprocessing/       # Stanza/spaCy pipelines for text normalization
│   ├── 02_feature_extraction/  # Implementation of 24 linguistic features (Syntactic/Lexical)
│   ├── 03_baselines/           # Dummy, Linear Regression, and Logistic Regression baselines
│   ├── 04_feature-based_models/# Non-neural Ordinal models (MLP + CORAL/CORN on manual features)
│   ├── 05_deep_models/         # Fine-tuning XLM-RoBERTa with various loss heads (The core models)
│   ├── 06_fusion/              # Early and Late fusion experiments
│   └── 07_visualizations/      # Generation of Confusion Matrices and Error Analysis plots
├── requirements.txt            # Python dependencies
└── README.md                   # Project documentation
```

## Reproducibility

Environment:
- Python 3.12
- PyTorch 2.x
- HuggingFace Transformers
- Scikit-learn

Deep models can be trained using the notebooks in `05_deep_models/`.

Random seeds are fixed for reproducibility (seed=42).

To run the deep learning experiments:

```bash
pip install -r requirements.txt
python -m spacy download ru_core_news_md
python -c "import stanza; stanza.download('ru')"
```

## Evaluation Metrics

Models are evaluated using:

- Accuracy
- Macro-F1
- Quadratic Weighted Kappa (QWK)
- Mean Absolute Error (MAE)


## Data Availability

The dataset used in this study contains learner essays collected within an institutional setting and cannot be publicly released due to privacy agreements. 

However, the `notebooks/` directory includes full preprocessing and modeling pipelines that can be applied to any comparable proficiency-annotated dataset (e.g., standard AES corpora).



## Citation

If you use this code, please cite the thesis:

```bibtex
@mastersthesis{gorbachev2026russianAES,
  author  = {Nikolai Gorbachev},
  title   = {Automated Essay Scoring for Russian as a Second Language: A Deep Ordinal Learning Approach},
  school  = {University of Bologna},
  year    = {2026},
  address = {Bologna, Italy}
}
```