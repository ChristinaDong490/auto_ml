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

