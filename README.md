# auto_ml

## H2O AutoML
### 1. Setup 
Target: total_lift
AutoML framework: H2O AutoML (Python API)
Max models per run: 10
Sort metric: RMSE

### 2. Top 5 Features
Extracted from GBM_5_AutoML_2_20250721_213707:
| Rank | Feature  |
|------|----------|
| 1    | backsq |
| 2    | deadlift   |
| 3    | candj   |
| 4    | snatch   |
| 5    | gender   |

### 3. Top 3 Models per Validation Score

#### Using All Features:

| Rank | Model ID                         | RMSE  | MAE   | Notes                   |
|------|----------------------------------|-------|-------|-------------------------|
| 1    | StackedEnsemble_BestOfFamily_1  | 3.273 | 1.738 | Best overall performance |
| 2    | StackedEnsemble_AllModels_1     | 3.505 | 1.648 | Slightly behind top     |
| 3    | DeepLearning_1                  | 4.532 | 2.223 | Good performance        |

#### Using Top 3 Features (backsq, deadlift, candj):

| Rank | Model ID                         | RMSE  | MAE   | Notes                         |
|------|----------------------------------|-------|-------|-------------------------------|
| 1    | StackedEnsemble_BestOfFamily_1  | 3.273 | 1.738 | Slight drop from full model   |
| 2    | StackedEnsemble_AllModels_1     | 3.505 | 1.648 | Similar trend                 |
| 3    | DeepLearning_1                  | 4.532 | 2.223 | Consistent rank               |

**Observation:** Top 3 models remain unchanged between feature sets, with better performance using **all features**.

### 4. Top 3 Models per Speed (Estimated)

Note: Speed inferred based on model type, as H2O AutoML does not show training time directly.

#### Using All Features:

| Rank | Model Type (ID) | Speed Rank | Notes                    |
|------|------------------|------------|--------------------------|
| 1    | GLM_1            | Fastest | Linear model, fastest    |
| 2    | GBM_5            | Medium | Gradient boosting trees  |
| 3    | DeepLearning_1   | Slower | Neural net, slower train |

#### Using Top 3 Features:

| Rank | Model Type (ID) | Speed Rank | Notes                            |
|------|------------------|------------|----------------------------------|
| 1    | GLM_1            | Fastest | Even faster with fewer features |
| 2    | GBM_5            | Medium | Fewer splits = faster           |
| 3    | DeepLearning_1   | Slower | Still heavy, but improved       |

**Observation:** Speed ranks are consistent across feature sets, but reduced features **improve speed overall**.

## MLJAR AutoML
### 1. Setup
The experiment was conducted using the MLJAR Supervised AutoML framework with the following configuration:  
automl = AutoML(  
    total_time_limit=600,         # Total training time limit: 10 minutes  
    mode="Perform",               # Balanced mode for accuracy and speed  
    explain_level=2               # Full explanation including feature importance  
)
### 2. Dataset Preparation:
Dataset: athletes_cleaned.csv  
Target variable: total_lift  
Dropped irrelevant columns:['athlete_id', 'name', 'region', 'background', 'experience', 'schedule', 'howlong']  
Encoded categorical variables: gender, eat  
Missing values filled with 0  
### 3. MLJAR AutoML Features:
Algorithms used: Random Forest, LightGBM, Xgboost, CatBoost, Neural Network  

Built-in preprocessing:  
- Missing value imputation
- One-hot encoding (if needed)
- Feature selection

Built-in ensembling: Model stacking and hill climbing

Auto-generated output:
- Model leaderboard with RMSE, MAE
- Feature importance
- HTML report with visualizations

### 4. Best Model Using All Features
<img width="358" height="230" alt="image" src="https://github.com/user-attachments/assets/9f25ba3d-3d1c-4bb9-8510-60bbabb7588e" />

### 5. Top 5 Features
<img width="784" height="546" alt="image" src="https://github.com/user-attachments/assets/3436c854-fa1f-4b7e-a8ed-c62b48d72a0a" />

### 6. Models with Top 3 Features
<img width="183" height="231" alt="image" src="https://github.com/user-attachments/assets/b0324d7e-c02a-4543-bfbc-0b15cc472f4b" />

### 7. Platform Type: Full-Code
MLJAR Supervised AutoML is considered a full-code AutoML platform.

**Reasons:**  
Requires Python coding to load data, define features, and run training.

All configuration (e.g., time limits, mode, metric) is done in code.

There is no GUI or drag-and-drop interface, and model deployment requires further engineering effort.

However, it significantly reduces boilerplate code for preprocessing, model selection, tuning, and reporting.

**Conclusion:**  
MLJAR provides a fully programmable AutoML pipeline ideal for data scientists who prefer fine control in notebooks or scripts while skipping tedious tuning and model management.

