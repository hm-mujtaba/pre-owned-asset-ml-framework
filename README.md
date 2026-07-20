# A Machine Learning Framework for Pre-Owned Asset Analysis: A Case Study on Used Cars

## Overview

This repository presents a machine learning framework for analyzing the pre-owned vehicle market, developed and validated as a case study using real-world listing data collected from PakWheels. The framework integrates the complete machine learning pipeline, including data acquisition, preprocessing, exploratory data analysis, comparative benchmarking, predictive modeling, missing-attribute estimation, and market analytics.

The project was developed as an academic research study and is currently being finalized for publication. While the framework is designed with broader applicability in mind, the present implementation and validation are limited to used cars.

---

## Features

- **Data Acquisition**
  - Selenium-based web scraper for PakWheels
  - Automatic recovery from browser interruptions
  - Incremental storage using SQLite

- **Data Preprocessing**
  - Price normalization (Lacs/Crore → PKR)
  - Vehicle specification extraction
  - Company and model extraction from listing titles
  - Duplicate and missing-value handling

- **Exploratory Data Analysis**
  - Price, mileage, and year distributions
  - City-wise market comparison
  - Fuel type and transmission analysis
  - Correlation analysis of numerical features

- **Model Benchmarking**
  - Decision Tree encoder comparison (Ordinal vs OneHot)
  - KNN encoder comparison
  - KNN neighbor-search algorithm benchmarking
  - Decision Tree hyperparameter optimization using GridSearchCV
  - Manual validation to identify and reject overfitted configurations

- **Machine Learning**
  - Decision Tree Regression for vehicle price prediction
  - K-Nearest Neighbors for missing attribute estimation

- **Market Analytics**
  - Segment-wise error analysis
  - Saleability assessment based on predicted market value
  - Listing evaluation for underpriced, fairly priced, and overpriced vehicles

---

## Repository Structure

```text
pre-owned-asset-ml-framework/
│
├── used_car_price_prediction.ipynb
├── knn_configuration_benchmark.ipynb
├── decision_tree_encoder_benchmark.ipynb
├── hyper_parameter_tuning.ipynb
│
├── pakwheels_dataset.db
├── grid_search_results.csv
├── segment_wise_error_summary.csv
│
├── report_feature_figures/
│   ├── city_distribution.png
│   ├── correlation_heatmap.png
│   ├── ...
│
├── result_evaluation_figures/
│   ├── actual_vs_predicted_price.png
│   ├── segment_wise_mae.png
│   └── segment_wise_mape.png
│
├── README.md
├── requirements.txt
├── LICENSE
└── .gitignore
```

---

## Methodology

### 1. Data Acquisition

- Scraped used vehicle listings from PakWheels
- Collected listings from Lahore, Karachi, and Islamabad
- Stored scraped data incrementally in SQLite for fault tolerance

### 2. Data Preprocessing

- Converted price strings into numeric PKR values
- Extracted structured vehicle specifications
- Parsed company and model names
- Removed duplicates and cleaned missing values

### 3. Exploratory Data Analysis

Performed exploratory analysis to understand:

- Price distribution
- Mileage distribution
- Year distribution
- Company and model popularity
- City-wise pricing
- Fuel type distribution
- Transmission distribution
- Feature correlations

### 4. Machine Learning

#### Price Prediction

A Decision Tree Regressor was trained to estimate used-car prices using structured vehicle attributes.

Evaluation metrics include:

- Mean Absolute Error (MAE)
- Mean Absolute Percentage Error (MAPE)
- Coefficient of Determination (R²)

#### Missing Attribute Estimation

A K-Nearest Neighbors model estimates missing listing attributes from partially available vehicle information.

---

## Benchmarking

Rather than selecting model configurations by default, this project performs dedicated benchmarking experiments.

### Decision Tree Encoder Benchmark

Compares:

- OrdinalEncoder
- OneHotEncoder

Evaluation criteria:

- Prediction accuracy
- Memory usage
- Feature dimensionality
- Training time
- Prediction time

OrdinalEncoder was selected because it achieves comparable predictive performance while significantly reducing feature dimensionality and computational cost.

---

### KNN Configuration Benchmark

Two independent experiments were performed.

**Encoder Comparison**

- OneHotEncoder
- OrdinalEncoder

OneHotEncoder was selected because KNN relies on distance calculations, where arbitrary ordinal relationships can distort similarity measurements.

**Neighbor Search Algorithm Benchmark**

Compared:

- Auto
- Brute
- KD Tree
- Ball Tree

The Brute algorithm was selected based on runtime analysis and dataset characteristics.

---

### Hyperparameter Optimization

Decision Tree hyperparameters were optimized using GridSearchCV.

Candidate models were additionally inspected manually to compare training and validation performance, allowing overfitted configurations to be rejected despite favorable cross-validation scores.

---

## Technologies Used

### Programming Language

- Python

### Libraries

- pandas
- NumPy
- scikit-learn
- matplotlib
- seaborn
- Selenium
- BeautifulSoup

### Database

- SQLite

---

## Results

Current evaluation on approximately **2,526 cleaned vehicle listings**.

| Metric | Value |
|---------|--------|
| R² | 0.83 |
| MAE | PKR 862,676 |
| MAPE | 17.92% |

These values correspond to the current implementation and may be updated as the research is finalized.

---

## Installation

Clone the repository

```bash
git clone https://github.com/hm-mujtaba/pre-owned-asset-ml-framework.git
```

Install dependencies

```bash
pip install -r requirements.txt
```

Launch Jupyter Notebook

```bash
jupyter notebook
```

---

## Usage

Execute the notebooks in the following order:

1. `used_car_price_prediction.ipynb`
2. `decision_tree_encoder_benchmark.ipynb`
3. `knn_configuration_benchmark.ipynb`
4. `hyper_parameter_tuning.ipynb`

The benchmarking notebooks are independent experiments used to justify the configuration choices adopted in the primary machine learning pipeline.

---

## Project Status

**Active Development**

Current work includes:

- Finalizing model optimization
- Updating evaluation metrics
- Completing the accompanying IEEE research paper
- Supervisor review and publication preparation

---

## Future Work

- Extend the framework to additional categories of pre-owned assets
- Benchmark additional regression algorithms
- Improve missing-attribute estimation techniques
- Develop a lightweight decision-support application

---

## License

This project is licensed under the MIT License.
