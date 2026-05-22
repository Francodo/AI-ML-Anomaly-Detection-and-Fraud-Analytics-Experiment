Fraud Detection & Analytics — Exploratory Data Analysis

Foundational EDA experiment for building AI/ML fraud detection models. The process is applicable to any domain where the focus is fraud detection. We need to apply domain specific data with features that drive insights that alligns with the main goal.


Overview
This experiment performs Exploratory Data Analysis (EDA) on a real-world fraud transaction dataset to uncover patterns, surface anomalies, and develop intuition about the structure of fraudulent behavior. The insights and feature understanding gained here establish the analytical foundation for downstream AI/ML fraud detection modeling.
This work is part of the broader Bank Credit Card /and or / Healthcare Multi-Agent System with Claims Fraud Detection platform — specifically the data intelligence layer that feeds the Claims Fraud Detection Agent.

Objective

Perform rigorous EDA on a real-world fraud dataset to:

- Understand the dataset structure, variable types, and data quality
- Compute summary statistics to characterize distributions and outliers
- Identify fraud patterns through targeted visualizations
- Build analytical intuition that will guide feature engineering and model selection
- Establish a reproducible EDA baseline for future modeling experiments


The output of this experiment directly informs:

- Feature selection for fraud detection models (Claim Billing Fraud, Upcoding Detection, Network Anomaly, Identity Verification, Duplicate Claim)
- Threshold calibration for the Fraud Risk Scoring Engine
- Data quality requirements for the Semantic Layer's Claims Data Pipeline


Dataset


Experiment Steps
Step 1 — Load the Dataset

- Import raw transaction/claims data from source files (CSV / Parquet / DB)
- Verify file integrity, encoding, and schema alignment
- Apply initial data type inference and column mapping

Step 2 — Explore Structure & Summary Statistics

- Inspect shape, dtypes, and memory footprint
- Compute descriptive statistics: mean, median, std, min/max, quartiles
- Identify missing values, null ratios, and cardinality per feature
- Examine class imbalance between fraud and non-fraud labels
- Profile categorical features (top-N frequencies, rare categories)

Step 3 — Visualize Fraud Patterns
📦 Boxplots

Compare distributions of transaction amounts, claim values, and billing codes between fraud and non-fraud classes
Surface outliers and extreme values that characterize fraudulent transactions
Detect skew and spread differences across claim types

📊 Histograms

Visualize frequency distributions of continuous features (claim amounts, service dates, procedure counts)
Identify bimodal distributions or heavy tails that signal anomalous billing behavior
Overlay fraud vs. non-fraud distributions to highlight separability

🌡️ Heatmap

Compute and visualize the correlation matrix of numerical features
Identify multicollinearity and feature redundancy
Highlight features most correlated with the fraud target label

📈 Additional Visualizations

Time-series plots — Fraud rate over time; detect seasonal or cyclical fraud surges
Bar charts — Fraud rate by provider, claim type, specialty, and payer
Scatter plots — Claim amount vs. service units, colored by fraud label
Count plots — Fraud label distribution; procedure code frequency by fraud class
KDE plots — Kernel density estimates for continuous features by fraud class

📋 Summary

Consolidate key EDA findings into a structured insights table
Document feature-level fraud signals identified during analysis
Flag data quality issues (missing data, outliers, inconsistencies) for the pipeline team
Formulate hypotheses for feature engineering in the modeling phase

🖥️ Dashboard

- Assemble an interactive EDA dashboard combining key charts and statistics
- Enable filtering by fraud label, date range, claim type, and provider
- Provide at-a-glance fraud pattern summaries for data science and fraud analytics teams

# 1. Install dependencies
pip install -r requirements.txt

# 2. Launch Jupyter
jupyter notebook notebooks/

# 3. Run notebooks 

📊 Key EDA Outputs
OutputDescriptionfraud_summary_stats.csvDescriptive statistics for all features, split by fraud labelcorrelation_heatmap.pngFeature correlation matrix highlighting fraud-related signalsamount_distribution.pngClaim amount distributions: fraud vs. legitimatefraud_rate_by_provider.pngProvider-level fraud rate rankingfraud_timeline.pngFraud volume and rate over timeeda_dashboard.htmlInteractive Plotly dashboard for full EDA explorationeda_findings_report.mdStructured summary of insights, anomalies, and modeling hypotheses

Analytical Findings 
Document key findings here as the experiment progresses:

- Class imbalance — Fraud labels represent approximately X% of all transactions; SMOTE or class weighting will be required for modeling.
- Amount distribution — Fraudulent claims show a [higher/lower/bimodal] amount distribution vs. legitimate claims (p-value: X).
- Top correlated features — [feature_1], [feature_2], and [feature_3] show the strongest correlation with the fraud label.
- Provider anomalies — Provider IDs [X, Y, Z] exhibit disproportionate fraud rates, suggesting targeted investigation.
- Temporal patterns — Fraud rate spikes observed in [time period], consistent with [seasonal / campaign-driven] fraud behavior.


Connection to Fraud Detection Platform
This EDA experiment feeds directly into the Healthcare Multi-Agent System fraud pipeline:
Cloud Data Sources (AWS / Azure / GCP)
        ↓
  Semantic Layer (Feature Store · Claims Data Pipeline · ML Feature Engineering)
        ↓
  Claims Fraud Detection Agent
        ↓
  ┌─────────────────────────────────────────┐
  │  Fraud Detection Models                 │
  │  ├── Claim Billing Fraud Model  ◄───────┼── EDA informs features
  │  ├── Upcoding & Unbundling      ◄───────┼── EDA informs thresholds
  │  ├── Network Anomaly Model      ◄───────┼── EDA identifies provider signals
  │  ├── Identity Verification      ◄───────┼── EDA flags member anomalies
  │  └── Duplicate Claim Model      ◄───────┼── EDA surfaces duplicate patterns
  └─────────────────────────────────────────┘
        ↓
  Fraud Risk Scoring & Alert Engine
        ↓
  SIU Escalation / Case Queue
