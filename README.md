📌 Project Overview

This project presents an end-to-end machine learning and bioinformatics pipeline for analyzing gene expression data to study Cystic Fibrosis.

The system integrates multiple RNA-seq datasets, applies statistical and machine learning techniques, and extracts biological insights such as biomarkers and disease activity.

🎯 Objectives
Classify samples as CF vs Healthy using gene expression data
Identify differentially expressed genes (DEGs)
Extract key biomarker genes
Measure disease intensity using CF Activity Score
Evaluate model generalization across datasets
Analyze domain shift in biological data
📊 Datasets Used
1. Processed Dataset
Source: NCBI GEO (GSE127696)
Type: RNA-seq expression matrix
Contains labeled samples (CF vs Healthy)
2. Raw Dataset
Source: HTSeq count files (49 samples)
Type: Raw RNA-seq counts
Requires preprocessing and merging
🧠 Why These Datasets?
Both datasets are RNA-seq (same modality) → same feature type (genes)
Enables cross-dataset validation
Simulates real-world variability across experiments
⚙️ Pipeline Overview
Data Collection
    ↓
Preprocessing & Normalization
    ↓
Gene Alignment
    ↓
Differential Gene Expression (DGE)
    ↓
Feature Selection
    ↓
Scaling + PCA
    ↓
Model Training (Random Forest)
    ↓
Validation (CV + Shuffle Test)
    ↓
Cross-Dataset Evaluation
    ↓
Biomarker Extraction
    ↓
CF Activity Score
    ↓
Visualization & Insights
🧹 Data Preprocessing
Removal of invalid/low-expression genes
Log transformation: log2(x + 1)
Merging of raw HTSeq files into expression matrix
Conversion to sample × gene format
🔗 Gene Alignment
Converted Ensembl IDs → Gene Symbols
Identified common genes (~13,904)
Ensured consistent feature space across datasets
🔬 Differential Gene Expression (DGE)

Performed statistical analysis to identify significant genes:

t-test
Mann–Whitney U test
Fold change analysis
FDR correction

👉 Output: Genes significantly different between CF and Healthy

🎯 Feature Selection
Method: SelectKBest (ANOVA F-test)
Selected top 500 genes

👉 Purpose:

Reduce noise
Improve model performance
Focus on biologically relevant features
📉 Dimensionality Reduction
StandardScaler applied

PCA used to reduce:

500 genes → 50 components

👉 Purpose:

Remove redundancy
Improve computational efficiency
🤖 Model
Algorithm: Random Forest
Why Random Forest?
Handles high-dimensional data well
Robust to noise
Captures non-linear relationships
Requires minimal tuning
📊 Validation Strategy
1. Train-Test Split
Evaluates performance on unseen data
2. Cross-Validation
Ensures model stability across splits
3. Shuffle Test (Critical)
Randomizes labels
Confirms model is learning real biological signal
🌍 Cross-Dataset Evaluation
Model trained on Dataset 1
Tested on Dataset 2
Observation:
Predictions biased toward one class
Low confidence (~0.56)

👉 Indicates domain shift between datasets

🧬 Biomarker Extraction
Extracted top genes using feature importance
Identified genes contributing most to classification

👉 Provides biological interpretability

🧠 CF Activity Score
Computed as average expression of top biomarker genes

👉 Converts:

Binary classification → continuous disease intensity
📊 Visualizations
PCA plots (class separation)
UMAP (non-linear structure)
Heatmaps (gene patterns)
Volcano plot (DGE results)
Confusion matrix (model evaluation)
Feature importance plots
Activity score distributions
🔍 Key Findings
Model achieves high accuracy (~94%)
Stable across cross-validation
Not overfitting (validated via shuffle test)
Identified key biomarker genes
Activity score reflects disease intensity
Domain shift observed across datasets
⚠️ Limitations
Small sample size
External dataset lacks labels
Domain shift affects generalization
PCA reduces interpretability
🚀 Future Work
Integrate more datasets
Use pathway-level analysis (e.g., KEGG, GO)
Apply deep learning models
Improve domain adaptation techniques
Include clinical metadata
💎 Conclusion

This project demonstrates that gene expression data can effectively distinguish cystic fibrosis samples and identify key biomarkers. However, cross-dataset evaluation highlights variability in biological data and the importance of robust validation.

🛠️ Tech Stack
Python
Pandas, NumPy
Scikit-learn
Seaborn, Matplotlib
SciPy, Statsmodels
