# Detecting Intoxication from Smartphone Accelerometer Data

## Quick Results

| Metric | Value |
|---------|------:|
| Best Model | Bagging |
| Best Accuracy | **76.94%** |
| Models Evaluated | 8 |
| Raw Dataset Size | **14,058,282** readings |
| Preprocessed Dataset Size | **2840** readings |

---

## Highlights

* Processed **14,057,567** smartphone accelerometer readings collected from **13** participants
* Engineered features from raw accelerometer data by computing **vector magnitude** and **weighted average** across *120-second windows*
* Aligned values across multiple datasets
* Trained and compared **7** machine learning classification models (*Logistic Regression, Classification Trees, Random Forests, Bagging, Boosting, Support Vector Machines, and K-Nearest Neighbors*)
* Explored **1** unsupervised learning model (*Hierarchical Clustering*)
* Evaluated performance using **accuracy**, **precision**, **recall**, and **F1-score**
* Best-performing model achieved **76.94%** accuracy
* Conducted exploratory data analysis and feature visualization to understand movement patterns

---

## Overview

This project aims to determine whether we can detect excessive alcohol consumption using only smartphone accelerometer data for the 13 participants included in the *Bar Crawl: Detecting Heavy Drinking* dataset. Heavy drinking poses significant health risks; being able to identify when someone is approaching or experiencing high levels of intoxication offers the potential to intervene earlier and reduce alcohol-related harm. 

Our objective is to determine whether accelerometer-based models can identify alcohol intoxication without relying on direct biochemical measurement. By examining whether movement patterns recorded through smartphone sensors correlate with elevated Transdermal Alcohol Content (TAC) levels, we hope to evaluate the feasibility of a non-invasive, automated detection system.

---

## Dataset

**Source**

The dataset used for the project was retrieved from the *UC Irvine Machine Learning Repository*: [Bar Crawl: Detecting Heavy Drinking](https://archive.ics.uci.edu/dataset/515/bar+crawl+detecting+heavy+drinking)

**Description**

The dataset contains **13** participants. For each participant, TAC level was retrieved every 20-30 minutes and smartphone accelerometer data (x, y, z) was recorded every ~0.5 seconds over a 24-hour period. This resulted in a TAC dataset of **715** observations, and an accelerometer dataset of **14,057,567** observations.

Each TAC and accelerometer reading is marked with a timestamp and participant ID to facilite data alignment.

**Preprocessing**

Raw TAC data was transformed into classification data, with the specified user being classified as sober **(TAC < 0.08)** or intoxicated **(TAC ≥ 0.08)** for the corresponding time of the TAC reading.

Raw accelerometer data was first averaged across **120-second windows** for each participant ID to reduce dataset size. Next, the average **x**, **y**, and **z** accelerometer readings of each interval were combined into a single vector magnitude variable.

Averaged accelerometer values were labeled as `sober` or `intoxicated` depending on which TAC reading occurred **closest** to the start of the interval. If no TAC readings were recorded within **15 minutes** of the start of the interval, that interval was **removed** from the dataset.

The data was split into training and testing data using a **80 / 20** split.

---

## Methodology

### Feature Engineering

The following methods were used to reduce dataset size and improve model performance.

* Vector Magnitude
* Windowed averages

---

### Machine Learning Models

| Model | Purpose |
|--------|----------|
| Logistic Regression | Interpretable baseline for binary classification that estimates how accelerometer features relate to intoxication |
| Decision Tree | Captures nonlinear feature interactions and provides an interpretable decision-making process |
| Random Forest | Reduces overfitting by averaging many decision trees, improving predictive performance and robustness |
| Bagging |  Improves model stability by combining multiple bootstrap-trained decision trees |
| Boosting | Sequentially builds trees that focus on difficult examples, often improving predictive accuracy |
| Support Vector Machine | Maximizes the margin between classes and can model nonlinear relationships using kernel functions |
| K-Nearest Neighbors | Classifies observations based on nearby examples in feature space, capturing local movement patterns associated with intoxication |

Some of the models listed above allowed for hyperparameter tuning. For each of these we compared model performance against different values, kernel types, tress depths, and used cross validation to determine the proper parameters for our models. *More information can be found in the final report.*

---

## Results

### Model Performance

| Model | Accuracy | Precision | Recall | F1 Score |
|--------|----------|-----------|--------|----------|
| Logistic Regression | 0.6954 | 0.5472 | 0.1629 | 0.2511 |
| Decision Tree | 0.6567 | 0.4719 | 0.8034 | 0.5946 |
| Random Forest | 0.7676 | 0.6162 | 0.6854 | 0.6489 |
| **Bagging**| **0.7694** | **0.6169** | **0.6966** | **0.6544** |
| Boosting | 0.7606 | 0.6105 | 0.6517 | 0.6304 |
| SVM | 0.6972 | 0.5625 | 0.1517 | 0.2389 |
| KNN | 0.7130 | 0.5510 | 0.4551 | 0.4985 |
| HC | 0.6331 | 0.3459 | 0.0719 | 0.1191 |

---

## Project Pipeline

```text
Raw Accelerometer Data
          ↓
    Data Cleaning
          ↓
  Window Aggregation
          ↓
 Feature Engineering
          ↓
  Train/Test Split
          ↓
    Model Training
          ↓
   Model Evaluation
```

---

## Repository Structure

```
.
├── README.md
├── LICENSE
│
├── docs/
│   └── index.html
│
├── data/
│   └── average_accel.csv
│
├── notebooks/
│   └── DetectingIntoxication.Rmd
│
└── report/
    └── Final_Report.pdf
```

---

## Running the Project

### Technologies

- R
- RStudio (recommended)

### Required Packages

```r
library(randomForest)
library(gbm)
library(tree)
library(e1071)
library(class)
library(ggplot2)
```

Or install everything using

```r
install.packages(c(
  "randomForest",
  "gbm",
  "tree",
  "e1071",
  "class",
  "ggplot2"
))
```

### Run

Open

```
notebooks/DetectingIntoxication.Rmd
```

and knit the notebook, or execute the code chunks sequentially.

---

## R Notebook

The rendered HTML page from the R markdown file can be viewed here: [Intoxication Detection Project](https://elsanorm17.github.io/detecting-intoxication/)

---

## Report

The complete technical report describing the methodology, experiments, and results is available in:

```
report/Final_Report.pdf
```

---

## Limitations

* Limited sampling size (only 13 participants) — model performance may not generalize to unseen populations
* Imbalanced class sizes
* Features were manually engineered
* Only averaged accelerometer data was considered

---

## Future Improvements

Potential future work includes:

* More sophisticated feature engineering
* Deep learning models (LSTM/Transformer) for sequential sensor data
* Subject-independent cross-validation
* Dataset with larger participant group

---

## My Contributions

This repository is maintained as part of my Computer Science projects portfolio.

My primary contributions included:

* Data cleaning, window aggregation, and feature engineering
* Research and selection of appropriate classification models
* Hyperparameter tuning
* Model performance analysis and comparison
* Wrote the *Dataset*, *Research Question/Problem*, *Data Preprocessing*, *Proposed Methods*, and *Summary* portions of the Final Report

The original project was completed collaboratively for a university machine learning/statistics course.

---

## What I Learned

* Challenges of working with large, noisy, real-world datasets
* Importance of feature engineering for sensor data
* Evaluating models beyond simple accuracy
