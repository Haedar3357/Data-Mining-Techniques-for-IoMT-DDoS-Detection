#  Data Mining Techniques for IoMT DDoS Detection

##  Project Overview

This research project explores **data mining and machine learning techniques** for the detection and classification of IoMT (Internet of Medical Things) cyber attacks. Focusing on the **MQTT-DDoS-Connect_Flood** attack type, the project applies both **supervised and unsupervised models**, along with **feature selection methods**, to evaluate model performance and detect anomalous behavior in network traffic.

---

##  Objective

- Investigate the characteristics of benign and attack traffic in the **IoMT-2024 dataset**.
- Apply **data mining methods** to identify the most relevant features.
- Compare the performance of models trained on:
  - All features
  - A subset of **common important features** extracted using:
    - Pearson correlation
    - Chi-squared test
    - ANOVA F-test
- Evaluate multiple ML models for both classification and anomaly detection.
- Provide an insightful methodology for researchers and students working in cybersecurity.

---

##  Dataset Information

- **Source**: [UNB CIC - IoMT Dataset 2024](https://www.unb.ca/cic/datasets/iomt-dataset-2024.html)
- **Attack Studied**: `MQTT-DDoS-Connect_Flood`
- **Samples**:
  - Benign: 192,732
  - Attack: 173,036
- **Features**:
  - 46 numeric features
  - No missing or categorical values

---

##  Project Workflow

### 1. Data Preparation

- Combined benign and attack data into a single dataset.
- Verified data integrity (no nulls or constant columns).
- Scaled data using `MinMaxScaler`.

### 2. Feature Selection (Data Mining)

Three different techniques were used to identify influential features:
- **Correlation with target label** (Pearson > |0.3|)
- **Chi-square test** (Top 14 ranked)
- **ANOVA F-test** (Top 14 ranked)

> The **intersection** of the three methods was taken to form the final subset of features.

### 3. Data Distribution Analysis
- Conducted a comprehensive statistical analysis to examine the distribution of features using tests like the Anderson-Darling test.

- Confirmed that the dataset’s features do not follow a normal distribution, which was consistent across benign, attack, combined, and filtered datasets.

- Attempted normalization and transformation techniques (Box-Cox and Yeo-Johnson) to approach normality, but some features remained non-normal.

- Based on these findings, decided to focus on tree-based ensemble models (Random Forest, Gradient Boosting) which are robust to non-normal data distributions, avoiding algorithms that assume normality (like Logistic Regression, SVM).

 ### 4. Outlier Detection and Data Cleaning
- Implemented multiple methods for detecting outliers in the dataset:

- Z-Score Method: Identifies outliers based on how many standard deviations a point is from the mean.

- Interquartile Range (IQR) Method: Detects outliers lying outside 1.5 times the IQR below Q1 or above Q3.

- Isolation Forest Algorithm: An unsupervised machine learning method effective in isolating anomalies.

- Cross-validated the detected outliers across all three methods to identify common anomalies.

### 5. Model Training and Evaluation

####  Supervised Models (on full and selected features)
- `Random Forest`
- `Gradient Boosting`

Both were trained and validated using:
- 80/20 train-test split
- Accuracy, Precision, Recall, F1-score
- Confusion Matrix

#####  Results:
| Model                  | Accuracy | Precision | Recall | F1-score |
|------------------------|----------|-----------|--------|----------|
| Random Forest (full)   | 100%     | 1.00      | 1.00   | 1.00     |
| Gradient Boosting (full)| 100%    | 1.00      | 1.00   | 1.00     |
| Random Forest (selected)| 100%    | 1.00      | 1.00   | 1.00     |
| Gradient Boosting (selected)| 100%| 1.00      | 1.00   | 1.00     |

> All models achieved **perfect classification** on the selected binary task, even with reduced features.

---

### 4. Unsupervised Learning & Anomaly Detection

####  KMeans Clustering
- Clustering into 2 groups using PCA-reduced data.
- Evaluated by comparing labels post-cluster matching.

**Accuracy**: `0.998`  
**Confusion Matrix**:
[[192394 338]
[ 393 172643]]



####  Isolation Forest
- Used for anomaly detection.
- Detected ~1% of samples as anomalies, matching expected attack distribution.



---

##  Insights

- Feature selection **reduced dimensionality** with **no performance degradation**.
- Models were extremely effective at distinguishing attack patterns.
- KMeans was surprisingly accurate for an unsupervised method.
- Isolation Forest successfully flagged attacks as anomalies without labeled supervision.

---

##  Requirements

**Main libraries:**

- scikit-learn

- numpy

- pandas

- matplotlib
---

## Citation

If using this work or the dataset, please cite:
IoMT Dataset – Canadian Institute for Cybersecurity

---
## Author
This project was built as part of a research initiative in the fields of cybersecurity, IoMT, and machine learning.

For any questions or suggestions, feel free to open an issue or submit a pull request.
