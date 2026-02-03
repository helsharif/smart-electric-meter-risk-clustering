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

* Mean and peak kWh
* Load variability and coefficient of variation
* Load ramp rates

### Voltage Stability

* Mean voltage
* Voltage standard deviation
* Frequency of voltage excursions

### Frequency Stability

* Mean frequency
* Frequency deviation from nominal
* Frequency variability

### Operational Stress Proxies

* Voltage–current correlation
* Day vs night load ratios
* Event counts (spikes, drops)

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

---

## 📈 Cluster Interpretation

Clusters are analyzed and labeled based on their power-quality signatures, for example:

* **Stable Load / Stable Voltage:** Likely healthy meters
* **High Load Variability:** Potential demand stress or customer behavior effects
* **Voltage Instability / Frequency Noise:** Possible feeder or transformer-level issues

These interpretations are framed in **operational terms**, rather than purely statistical labels.

---

## ⚙️ Operational & Business Value

This analysis demonstrates how utilities can use AMI data to:

* Proactively identify groups of meters with elevated outage risk
* Prioritize field inspections and asset maintenance
* Support targeted customer notifications during grid disturbances
* Improve grid reliability metrics through early detection

While this project does not perform outage prediction, it provides a **foundational segmentation layer** that can support downstream predictive models.

---

## 📁 Repository Structure

```
.
├── cleaned_data/
│   └── SM Cleaned Data BR2019.csv
├── notebooks/
│   ├── 01_feature_engineering.ipynb
│   ├── 02_kmeans_clustering.ipynb
│   └── 03_cluster_interpretation.ipynb
└── README.md
```

---

## 🛠️ Tech Stack

* **Language:** Python
* **Data Analysis:** Pandas, NumPy
* **Machine Learning:** Scikit-learn
* **Visualization:** Matplotlib, Seaborn, Plotly
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



