# Unsupervised Clustering of AMI Power Quality Data for Meter Risk Segmentation

**Utility-focused k-means clustering project using real Advanced Metering Infrastructure (AMI) data** to segment smart meters by load behavior, voltage stability, and frequency characteristics. The project demonstrates how unsupervised learning can support **outage risk identification, asset health monitoring, and proactive grid operations**.

---

## 🚀 Project Highlights

* **Task:** Unsupervised clustering (k-means)
* **Domain:** Advanced Metering Infrastructure (AMI) analytics
* **Objective:** Segment meters by power-quality and load behavior
* **Techniques:** Feature engineering, k-means clustering, cluster validation
* **Data:** High-frequency real AMI telemetry (kWh, voltage, current, frequency)
* **Output:** Interpretable meter clusters linked to operational risk profiles

This repository emphasizes **business-relevant unsupervised learning**, aligned with how utilities analyze large fleets of smart meters at scale.

---

## ⚡ Motivation & Problem Statement

Electric utilities collect massive volumes of high-frequency AMI data, including energy usage, voltage, current, and frequency measurements. While this data is critical for grid visibility, it is often **underutilized for proactive reliability analytics**.

Manual inspection of individual meters is not scalable, and labeled outage data may be incomplete or unavailable.

**Goal:**
Use **unsupervised machine learning** to automatically group smart meters into behaviorally similar clusters that can help utilities:

* Identify meters exhibiting unstable voltage or load patterns
* Detect early indicators of outage risk or upstream asset stress
* Prioritize investigation, maintenance, and customer communication

---

## 📊 Dataset Description

The project uses **real AMI telemetry data** stored as:

```
cleaned_data/SM Cleaned Data BR2019.csv.zip
```

Each record represents a timestamped measurement from a smart meter and includes:

* `X_Timestamp`: Measurement timestamp
* `t_kWh`: Energy consumption
* `z_Avg Voltage (Volt)`: Average voltage
* `z_Avg Current (Amp)`: Average current
* `y_Freq (Hz)`: Grid frequency
* `meter`: Meter identifier

High-frequency measurements allow the derivation of **power-quality signatures** for each meter.

**Data Source:**
**High frequency smart meter data from two districts in India (Mathura and Bareilly)**
Agrawal, S., Mani, S., Ganesan, K., and Jain, A. (2021)
https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/GOCHJH

---

## 🧠 Feature Engineering Strategy

Rather than clustering raw time-series data, this project aggregates measurements into **per-meter behavioral features**, which is standard practice in utility analytics.

Example engineered features include:

### Load Behavior
- Mean energy consumption  
- Load variability (coefficient of variation)  
- Energy ramp rates (mean and 95th percentile)  

### Voltage Stability
- Mean voltage  
- Voltage variability and ramping behavior  

### Frequency Stability
- Frequency excursion rate outside nominal tolerance  

### Electrical Stress & Coupling
- Mean and peak current  
- Voltage–current correlation  
- Energy–voltage correlation  

Each meter is represented as a **single feature vector**, enabling scalable fleet-level analysis.

---

## 🔍 Clustering Approach

### Why K-Means?

* Suitable for large, unlabeled AMI datasets
* Computationally efficient and scalable
* Produces interpretable cluster centroids
* Commonly used in utility segmentation workflows

### Methodology

* Feature standardization
* K-means clustering across multiple values of *k*
* Elbow method and silhouette scores for model selection
* Cluster stability checks using multiple random initializations

### Model Selection
K-means was evaluated across multiple values of *k* using both inertia (elbow method) and silhouette score.  
A final choice of **k = 4** was selected to balance mathematical separation with **operational interpretability**.

---

## 📉 Model Diagnostics

### Elbow Method
The elbow curve shows diminishing returns beyond four clusters, indicating a reasonable trade-off between compactness and complexity.

![Elbow Method for K-Means](results/K-Means Elbow Method Results.png)

### Silhouette Analysis
Silhouette scores indicate **moderate separation**, which is expected for real-world AMI behavioral data where meter characteristics vary along a continuum rather than forming perfectly distinct groups.

![Silhouette Analysis for K-Means](results/K-Means Silhouette Score Results.png)




---

## 📈 Cluster Results & Interpretation

### Cluster Feature Heatmap (Normalized Centroids)

The figure below shows **normalized (z-score) cluster centroids** across key load, voltage, frequency, and current features:

- **Red:** Above-average behavior relative to the meter population  
- **Blue:** Below-average behavior  
- **White:** Near-average behavior  

Each row represents a **behavioral fingerprint** for a cluster.

![Cluster Feature Heatmap](results/K-Means Cluster Normalized Heatmap Result.png)

### Cluster Narratives (k = 4)

- **Cluster 0 – Stable Baseline Meters**  
  Low energy consumption and ramping, with stable voltage and frequency behavior. Represents a healthy baseline population requiring minimal monitoring.

- **Cluster 1 – Demand-Variable, Low-Load Meters**  
  Low average consumption but high relative variability, likely driven by customer usage patterns rather than grid or asset stress.

- **Cluster 2 – Power-Quality Volatile Meters**  
  Elevated voltage variability, frequent frequency excursions, and strong voltage–load coupling. Indicative of upstream feeder or transformer-level stress and a high-priority group for reliability monitoring.

- **Cluster 3 – High-Load, High-Ramping Meters**  
  High consumption and rapid load changes with generally stable voltage and frequency. Important for capacity planning and understanding demand-driven stress amplification during peak events.

---

## ⚙️ Operational & Business Value

This analysis demonstrates how utilities can use AMI data to:

- Proactively identify groups of meters with elevated reliability risk  
- Prioritize field inspections and asset maintenance  
- Support targeted customer notifications during grid disturbances  
- Establish a segmentation layer for downstream outage prediction or asset health models  

This project provides a **foundational behavioral segmentation** aligned with real utility workflows.

---

## 📁 Repository Structure

```
.
├── cleaned_data/
│   └── SM Cleaned Data BR2019.csv
│   └── SM Resampled Data BR2019 30min.csv
├── notebooks/
│   ├── 01_feature_engineering.ipynb
│   └──  02_kmeans.ipynb
├── results/
│   ├── kmeans_cluster_centroids_z.csv
│   ├── K-Means Cluster Normalized Heatmap Result.png
│   ├── K-Means Elbow Method Results.png
│   └── K-Means Silhouette Score Results.png
└── README.md
```

---

## 🛠️ Tech Stack

* **Language:** Python
* **Data Analysis:** Pandas, NumPy
* **Machine Learning:** Scikit-learn
* **Visualization:** Plotly
* **Methods:** Feature engineering, k-means clustering, validation metrics

---

## 🔍 Reproducibility & Best Practices

* Clear separation of data preparation and modeling
* Scaled features for distance-based clustering
* Explicit cluster validation metrics
* Interpretable cluster summaries
* Modular notebook structure

---

## ⚠️ Disclaimer

This project is for **research and portfolio demonstration purposes only**. Results are illustrative and do not represent operational decisions for any specific utility.

---

## 👤 Author

**Husayn El Sharif**
Senior Data Scientist / Machine Learning Engineer

---

## 📌 Portfolio Relevance

This project highlights:

* Applied unsupervised learning with real utility data
* AMI-focused feature engineering
* Business-oriented interpretation of k-means results
* Grid reliability and outage-related analytics



