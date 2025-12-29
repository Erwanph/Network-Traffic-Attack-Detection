# Network Traffic Attack Detection

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-CatBoost%20%7C%20LightGBM-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Status](https://img.shields.io/badge/Achievement-Dataquest%20Objective%20Quest%202024%20Finalist-success?style=for-the-badge)

> **Team Hustler** - Objective Quest 2024  
> *A Machine Learning approach to fortify cybersecurity through intelligent network traffic analysis.*

---

## 📌 Table of Contents
- [About the Project](#-about-the-project)
- [Business Understanding](#-business-understanding)
- [Dataset & Features](#-dataset--features)
- [Methodology](#-methodology)
- [Results & Performance](#-results--performance)
- [Key Insights](#-key-insights)
- [Tech Stack](#-tech-stack)
- [The Team](#-the-team)

---

## 📖 About the Project

This project was developed as a solution for **Objective Quest 2024**, focusing on critical cybersecurity challenges. The primary objective was to build a robust *Machine Learning* model capable of classifying network traffic in real-time to distinguish between normal user activities and malicious cyberattacks.

We utilized an *ensemble learning* approach with **CatBoost** and **LightGBM**, enhanced by deep *feature engineering* and *threshold tuning* to effectively handle severe class imbalance in cyber threat data.

---

## 💼 Business Understanding

### The Problem
In the digital era, global network traffic volume exceeds 100 zettabytes annually. Cyberattacks such as **Bruteforce**, **Probing**, and **CryptoMining** are becoming increasingly complex and difficult to detect using conventional *rule-based* methods, especially when hidden within millions of benign data packets.

### Objectives
1.  **Early Detection**: Automate the identification of cyber threats.
2.  **High Accuracy**: Minimize *False Negatives* (missed attacks) and *False Positives* (flagging normal traffic as threats).
3.  **Scalability**: Deploy efficient models suitable for high-volume data processing.

---

## 📊 Dataset & Features

The dataset comprises **416,473 rows** and **43 features**, containing both normal traffic and various attack vectors.

**Classification Targets (Multiclass):**
*   `Benign` & `Background` (Normal Activity)
*   `Probing` (Vulnerability Scanning)
*   `Bruteforce` & `Bruteforce-XML` (Forced Login Attempts)
*   `XMRIGCC CryptoMiner` (Illegal Cryptocurrency Mining)

**Key Features:**
*   **Identity**: `origin_host`, `response_host`, `origin_port`, `response_port`
*   **Flow Metrics**: `flow_duration`, `packets_per_sec`, `bytes_per_sec`
*   **TCP Flags**: `SYN`, `ACK`, `FIN`, `RST`

---

## ⚙️ Methodology

We implemented an *end-to-end data science* workflow:

### 1. Data Preprocessing
*   **Rule-Based Imputation**: Addressed *missing values* using network logic (e.g., imputing `IAT` and `Packet Counts` based on feature correlations) rather than simple mean/median filling.
*   **Type Conversion**: Converted IP Hosts and Ports into *Categorical* data types to allow the model to treat them as unique entities rather than continuous numbers.

### 2. Feature Engineering (Performance Driver 🚀)
We engineered new features to enhance predictive power:
*   **Binary PSH Flags**: Detects aggressive data push patterns common in attacks.
*   **Host-Port Combinations**: Captures specific interactions between source IPs and destination ports.
*   **Frequency Encoding**: Flags how often a Host appears (attacks often exhibit anomalous frequency patterns).
*   **Port Service Type**: Groups ports based on common services (HTTP, SSH, FTP).

### 3. Model Selection
We benchmarked several algorithms and selected **Non-Linear Models** due to data complexity:
*   ❌ *Logistic Regression / SVM*: Failed to capture complex, non-linear attack patterns.
*   ✅ **CatBoost & LightGBM**: Chosen for superior performance, automatic handling of categorical features, and native *Class Weights* support.

---

## 📈 Results & Performance

Our best-performing model is the **CatBoost Classifier** utilizing a **Class Weights** strategy to address data imbalance.

| Metric | Score (Validation) |
| :--- | :--- |
| **Custom Scoring** | **0.872** |
| **Accuracy** | High on majority classes |
| **Recall (Attacks)** | Significantly improved after tuning |

**Threshold Optimization:**
We performed manual *Threshold Tuning* for each class. This resulted in a model that is far more sensitive to rare attacks (like *Probing*) without compromising accuracy on normal traffic.

---

## 💡 Key Insights

Based on *Feature Importance* analysis (SHAP/Feature Importance plot):
1.  **Host & Port are King**: `origin_host`, `response_host`, and `port` are the most critical predictors. Cyberattacks tend to target specific IPs or Ports repeatedly.
2.  **Communication Patterns**: Features like `Flow Duration` and `Flag Counts` (FIN/RST) are highly effective at distinguishing machine behavior (bots/attacks) from human behavior.
3.  **Minority Class Challenge**: Classes like *Probing* are difficult to distinguish from *Benign* traffic without aggressive *threshold tuning*.

---

## 🛠 Tech Stack

*   **Language**: Python
*   **Data Processing**: Pandas, NumPy
*   **Machine Learning**: CatBoost, LightGBM, Scikit-Learn
*   **Visualization**: Matplotlib, Seaborn
*   **Environment**: Jupyter Notebook

---

## 👥 The Team (Team Hustler)

*   **Mohamad Maulana Firdaus Ramadhana**
*   **Erwan Poltak Halomoan**
*   **Viktor Arsindiantoro Siringoringo**

*Institut Teknologi Bandung (ITB)*

---

*Interested in the technical details? Check out the [Full Report (PDF)](./Hustler_Laporan-Objective-Quest-2024.pdf) or run the [Notebook](./submission_notebook_Final.ipynb).*
