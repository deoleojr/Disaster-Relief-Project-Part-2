# Disaster Relief Project Part 2

## Introduction

In the wake of the devastating earthquake that struck Haiti in 2010, countless individuals were displaced, leaving them without shelter, food, or water. The aftermath presented significant challenges for rescue operations, particularly locating those needing assistance. With communication lines down and infrastructure severely damaged, the ability to quickly and accurately identify the locations of displaced persons became a critical priority.

This project builds on Part 1 to apply advanced classification methods to solve a data-mining problem: locating people who need help after Haiti’s Earthquake in 2010. The project aims to find an algorithm that can efficiently and accurately search thousands of geo-referenced images to locate blue tarps and communicate their locations to rescue workers on the ground in time to provide food and water to those in need. This phase focuses on analyzing and validating results using holdout data.

---

## Data Summary

The dataset consists of high-resolution geo-referenced imagery collected from aircraft flying over the affected areas in Haiti. It includes the following variables:

- **Class**: A categorical variable with five categories describing land types (Vegetation, Soil, Rooftop, Non-Tarp, and Blue-Tarp).
- **Red, Green, Blue**: Numerical variables representing the intensity of each color in the image pixels for each land category.

### Key Insights:

1. **Class Distribution**:
   - Vegetation and soil dominate the dataset.
   - Blue tarps, critical for locating displaced persons, are relatively rare.
2. **Color Channel Characteristics**:
   - Blue tarps exhibit distinct high blue values, enabling their detection.
   - Vegetation has high green values.
   - Soil and rooftops show distinctive red and green values.
3. **Class Imbalance**:
   - Blue tarps' rarity poses challenges for training models to detect them accurately among other classes.
   - Techniques like resampling, class weighting, or synthetic data generation were applied to address imbalance.

---

## Methodology

### Preprocessing:
- Addressed missing values in the Red and Blue channels through imputation.
- Normalized color intensity values for consistency.
- Handled class imbalance using resampling techniques.

### Model Training and Evaluation:

1. **Models Used**:
   - Logistic Regression
   - Linear Discriminant Analysis (LDA)
   - Quadratic Discriminant Analysis (QDA)
   - K-Nearest Neighbors (KNN)
   - Random Forest
   - Penalized Logistic Regression (Elastic Net)
   - Support Vector Machines (SVM) with different kernels

2. **Validation**:
   - 10-fold cross-validation to evaluate model robustness.
   - Metrics: Accuracy, Precision, Recall (Sensitivity), F1 Score, ROC-AUC.

3. **Threshold Selection**:
   - Determined optimal classification thresholds using ROC curve analysis to maximize Youden's J statistic (Sensitivity + Specificity - 1).

### Tools and Libraries:
- **R Programming**:
  - `tidyverse` for data manipulation and visualization.
  - `pROC` for ROC curve analysis.
  - `GGally` for exploratory data analysis.

---

## Results

### Cross-Validation Metrics (Updated):

| Model                  | Accuracy | Recall (TPR) | FPR   | Precision |
|------------------------|----------|--------------|-------|-----------|
| Logistic Regression    | 92.9%    | 93.0%        | 20.5% | 99.8%     |
| Linear Discriminant Analysis (LDA) | 94.7%    | 95.4%        | 91.1% | 99.2%     |
| Quadratic Discriminant Analysis (QDA) | 99.2%    | 99.6%        | 0.0%  | 99.2%     |
| K-Nearest Neighbors (KNN) | 99.2%    | 99.6%        | 77.0% | 99.2%     |

### Holdout Data Metrics (Updated):

| Model                  | Accuracy | Sensitivity (TPR) | Specificity (TNR) | Precision | Balanced Accuracy |
|------------------------|----------|-------------------|-------------------|-----------|-------------------|
| Logistic Regression    | 98.01%   | 97.99%            | 98.77%            | 99.98%    | 98.38%            |
| Linear Discriminant Analysis (LDA) | 98.40%   | 98.80%            | 85.14%            | 99.72%    | 91.97%            |
| Quadratic Discriminant Analysis (QDA) | 99.50%   | 99.64%            | 69.31%            | 99.43%    | 84.47%            |
| K-Nearest Neighbors (KNN) | 98.55%   | 98.80%            | 85.14%            | 99.72%    | 91.97%            |
| Random Forest          | 98.69%   | 99.00%            | 82.39%            | 99.67%    | 90.69%            |
| Elastic Net            | 98.16%   | 100.0%            | 0.0%              | 98.16%    | 50.00%            |

### Model Interpretations:

- **Best Performing Model**: Quadratic Discriminant Analysis (QDA)
  - Highest accuracy and recall across datasets.
  - Perfect handling of negatives (FPR = 0.000).

- **Alternatives**:
  - Logistic Regression and Random Forest provided reliable and generalizable results.
  - KNN and SVM with Polynomial Kernel require fine-tuning to improve performance.

- **Challenges**:
  - Elastic Net had thresholding issues, predicting all instances as positive.

---

## Conclusion

1. **Best Algorithm**:
   - Quadratic Discriminant Analysis (QDA) is the recommended model for blue tarp detection due to its superior performance metrics.

2. **Impact of Data Quality**:
   - High-quality preprocessing ensures robust model predictions. Addressing class imbalance and missing values is critical.

3. **Relevance of Metrics**:
   - Recall and Precision are key to ensuring blue tarp detection accuracy, minimizing false positives and negatives.

4. **Recommendations**:
   - Deploy QDA for blue tarp detection in disaster relief scenarios to maximize efficiency and effectiveness.
   - Further refine Logistic Regression and Random Forest for secondary implementations.

---

## Acknowledgments

This project uses data from the Haiti Earthquake disaster relief efforts and leverages advanced classification techniques to assist in rescue operations. Special thanks to the researchers and contributors for providing insights and tools to enhance the effectiveness of disaster response strategies.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.

