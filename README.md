# Single-Cell RNA-seq Cell Classification

A comparative machine-learning analysis for clustering and classifying cells from single-cell RNA sequencing data.

The project explores gene-expression data using exploratory data analysis, highly variable gene selection, dimensionality reduction, unsupervised clustering, supervised classification, and autoencoder-based feature extraction.

## Project objectives

- Explore the structure and quality of a single-cell RNA-seq dataset.
- Select highly variable genes to reduce noise and dimensionality.
- Compare PCA, t-SNE, and UMAP representations.
- Evaluate K-Means, agglomerative clustering, Gaussian mixture models, and self-organizing maps.
- Predict cell labels using several machine-learning classifiers.
- Compare models trained on highly variable genes, all genes, and autoencoder-derived latent features.

## Dataset

The analysis uses the following input files:

- `single_cell.h5ad`: complete single-cell expression dataset.
- `singlecell_train.csv`: labelled cells used for model training.
- `random_singlecell.csv`: example file containing cell labels.

The original datasets are not included in this repository because of file-size and/or data-sharing restrictions. Place authorised copies inside `data/raw/` before running the notebook.

## Analysis workflow

1. Data import and exploratory data analysis.
2. Assessment of gene expression, detected genes, total counts, and matrix sparsity.
3. Selection of 2,000 highly variable genes using the Seurat approach implemented in Scanpy.
4. Principal component analysis on the full dataset and highly variable genes.
5. Unsupervised clustering with:
   - K-Means
   - Agglomerative clustering
   - Gaussian mixture models
   - Self-organizing maps
6. Non-linear visualisation using t-SNE and UMAP.
7. Supervised cell classification using:
   - Ridge logistic regression
   - Lasso logistic regression
   - Elastic Net logistic regression
   - Multi-layer perceptron
   - Random Forest
   - Support Vector Machine
   - Gaussian Naive Bayes
   - XGBoost
   - K-Nearest Neighbours
8. Autoencoder-based dimensionality reduction followed by classification.
9. Comparison of model performance across preprocessing strategies.

## Main results

The best-performing methods depended on the preprocessing strategy:

- **Highly variable genes with PCA:** Random Forest achieved an accuracy of approximately **0.642**.
- **All genes without PCA:** XGBoost achieved an accuracy of approximately **0.636**.
- **Autoencoder latent features:** SVM achieved an accuracy of approximately **0.629**.

Random Forest, SVM, and XGBoost were the most robust classifiers across the evaluated pipelines. Gaussian Naive Bayes was the least stable model, especially when applied to autoencoder-derived features.

Based on the notebook conclusions, **XGBoost trained on raw/full-gene data was selected as the overall preferred model after hyperparameter optimisation**.

## Repository structure

```text
single-cell-rnaseq-cell-classification/
├── README.md
├── requirements.txt
├── .gitignore
├── scrna_cell_classification.ipynb
├── data/
│   └── README.md
└── results/
```

## Installation

Clone the repository and create a virtual environment:

```bash
git clone https://github.com/YOUR-USERNAME/single-cell-rnaseq-cell-classification.git
cd single-cell-rnaseq-cell-classification
python -m venv .venv
```

Activate the environment on Windows:

```powershell
.venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

## Usage

Place the required datasets in `data/raw/`, update the paths in the notebook if necessary, and launch Jupyter:

```bash
jupyter notebook notebooks/scrna_cell_classification.ipynb
```

Run the cells in order from the beginning to reproduce the analysis.

## Technologies

- Python
- Jupyter Notebook
- Scanpy and AnnData
- pandas and NumPy
- scikit-learn
- TensorFlow/Keras
- XGBoost
- UMAP and t-SNE
- Matplotlib

## Limitations and future improvements

- Perform broader hyperparameter optimisation.
- Use nested cross-validation for a less biased comparison.
- Compare additional train-validation splits.
- Train classifiers directly on highly variable genes in every branch.
- Improve the autoencoder architecture and training strategy.
- Include biological marker-gene interpretation for the predicted cell groups.

## Authors

LAB RATZ Group

## License

This project is intended for educational and academic use. Add an appropriate licence only after confirming that all group members agree and that the dataset and course materials can be redistributed.
