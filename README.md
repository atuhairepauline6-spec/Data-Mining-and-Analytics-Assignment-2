# DSC8307 Assignment 2 — Data Mining, Modeling and Analytics

**Programme:** Master of Science in Data Science and Analytics  
**Year:** 2  
**Semester:** Advent 2026  
**Course code:** DSC8307  
**Course:** Data Mining, Modeling and Analytics  
**Institution:** Uganda Christian University

## Overview

This repository contains the two Jupyter notebook projects for Assignment 2. The work uses the datasets supplied with the assignment and addresses the tasks set out in the assignment brief.

- **Project 1 – Wholesale customers:** segments 440 wholesale customers according to their annual spending patterns and considers how the distributor could serve the resulting groups.
- **Project 2 – Credit card fraud detection:** compares methods for ranking transactions for possible fraud investigation using a dataset containing 284,807 transactions, including 492 labelled fraud cases.

The notebooks are intended to be run from beginning to end. They include the analysis, modelling, evaluation and interpretation for each project.

## Repository structure

```text
DSC8307-Assignment-2/
├── data/
│   ├── wholesale-customers.csv
│   └── creditcard.csv
├── project1_wholesale_segmentation.ipynb
├── project2_credit_card_fraud.ipynb
├── requirements.txt
└── README.md
```

Keep the `data` folder and the notebooks in this arrangement. The notebooks use relative file paths to load the datasets.

## Project 1: Wholesale customer segmentation

### Objective

The objective is to group wholesale customers according to their annual spending behaviour and use the resulting profiles to suggest ways the distributor could serve different customer groups.

### Dataset

The `wholesale-customers.csv` dataset contains 440 customers. It includes annual spending in monetary units across six product categories:

- Fresh
- Milk
- Grocery
- Frozen
- Detergents_Paper
- Delicatessen

It also includes two categorical descriptors, `Channel` and `Region`.

### Analysis and methods

The notebook checks the dataset's dimensions, missing values, duplicate records and spending distributions. The six spending variables are transformed using `log1p` and standardised before clustering. The Hopkins statistic is calculated to assess whether the prepared data shows a tendency to form clusters.

Three clustering approaches are examined:

1. **K-means (partitioning):** candidate values of *k* are evaluated using clustering measures, including silhouette score, to support selection of a solution.
2. **Agglomerative hierarchical clustering:** Ward linkage and a dendrogram are used to examine the hierarchical grouping of customers.
3. **DBSCAN (density-based clustering):** a k-distance plot is used to guide the neighbourhood distance setting. DBSCAN can identify noise observations rather than assigning every customer to a cluster.

The notebook compares the methods and examines the selected K-means customer profiles using median spending in the original monetary units. Channel and Region can help describe the groups, but the spending variables form the basis of the segmentation.

### Interpretation

Cluster numbers are identifiers rather than customer types. Descriptive names and recommendations should be based on the spending profiles shown by the notebook. The recommendations are suggestions for how the distributor might tailor service; the dataset does not directly measure customer profitability, loyalty or future purchasing.

## Project 2: Credit card fraud detection

### Objective

The objective is to build and compare approaches that rank transactions for further fraud investigation, then evaluate the rankings against withheld fraud labels. A high anomaly score is an investigation signal, not proof that a transaction is fraudulent.

### Dataset

The `creditcard.csv` dataset contains 284,807 European card transactions recorded over two days in September 2013. There are 492 transactions labelled as fraudulent, approximately 0.172% of the data. Most input variables are anonymised PCA components, alongside `Time` and `Amount`.

### Analysis and methods

The notebook examines the dataset, missing values, duplicate records, class distribution and transaction amounts. It transforms the strongly skewed `Amount` feature and uses a stratified, grouped train/test split so identical feature rows are kept together.

The following approaches are compared:

1. **Statistical outlier baseline:** robust z-scores based on the median and median absolute deviation (MAD) are used to produce an anomaly ranking.
2. **Cluster-based anomaly detection:** MiniBatch K-means is fitted without using fraud labels. Distance to the nearest cluster centre is used as the anomaly score.
3. **Classification-based detection:** a class-weighted Random Forest is trained using the training labels to estimate fraud risk.

Evaluation includes average precision, ROC-AUC, precision and recall at selected review capacities, and precision-recall curves. These measures are useful for a highly imbalanced dataset, where accuracy alone can give a misleading impression of performance.

### Interpretation and responsible use

An unusual transaction is not necessarily fraudulent. It may be a legitimate purchase that differs from a customer's usual activity, while some fraudulent transactions may resemble ordinary transactions. Model scores should therefore support human review rather than automatically determine whether a transaction is fraudulent. The dataset is historical and its PCA features are anonymised, which also limits direct interpretation and generalisation to current transactions.

## Software and dependencies

The notebooks use Python and the packages listed in `requirements.txt`. The analysis uses common data science libraries, including:

- NumPy and pandas for data handling
- Matplotlib and Seaborn for visualisation
- scikit-learn for preprocessing, clustering, classification and evaluation
- SciPy for hierarchical clustering
- Jupyter and IPython for notebook execution

## How to run the notebooks

1. Clone or download this repository.
2. Open the repository's main folder in VS Code or Jupyter.
3. Create and activate a Python virtual environment (recommended).
4. Install the dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

5. Open `project1_wholesale_segmentation.ipynb` and run all cells from top to bottom.
6. Open `project2_credit_card_fraud.ipynb` and run all cells from top to bottom.

Run the notebooks with the repository's main folder as the working directory so that the relative paths to the files in `data/` resolve correctly. Select the same Python environment in VS Code that you used to install the dependencies.

## Limitations

The wholesale dataset contains 440 customers and annual spending measures. It does not provide profit margins, order frequency, customer lifetime value or reasons for purchasing. Clusters describe patterns in the supplied spending data and should not be treated as complete customer profiles.

The fraud dataset covers only two days in September 2013. The fraud class is very small, and the anonymised PCA variables limit feature-level interpretation. Results may also change with a different data split, model settings or transaction population. Further testing on more recent data would be needed before operational use.

## Data and attribution

The datasets are the files supplied for the DSC8307 Assignment 2. Please retain the dataset documentation supplied with the assignment when distributing the data. This repository is prepared for the course assessment and should be used in accordance with the university's academic integrity and submission requirements.
