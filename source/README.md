Stream A = using team stats only
Stream B = using player and team stats together

# Step 1: Load data 

Notebooks:
- 1A_load_data.ipynb
- 1B_load_data_player+team.ipynb

1. Grab player and team stats using [Github NBA API](https://github.com/swar/nba_api) from NBA.com/stats <img src="../data/image/2022-09-18-16-35-09.png">

2. Remove outlier seasons with games played (GP) <= 30 games or >= 60 games as we want the cutoff at around mid-season <img src="../data/image/2022-09-18-16-36-40.png">

3. Fix the datatypes to numeric / category / string such that we can drop them in sklearn pipeline

4. Split dataset into train and test set before any more EDA to prevent data leakage

# Step 2: ML workflow on train set
2 options to tackle class-imbalance:
- balance class weights
  - 2A_ML_workflow_class_balanced_average precision.ipynb
  - 2B_ML_workflow_class_balanced_average precision_player plus team.ipynb
- ADASYN for synthetic samples
  - 2A_ML_workflow_ADASYN_average precision.ipynb
  - 2B_ML_workflow_ADASYN_average precision_player plus team.ipynb

1. Exploratory data analysis 
   - class imbalance: 3% positive only <img src="../data/image/2022-09-18-16-46-15.png">
   - correlation matrix <img src="../data/image/2022-09-18-16-46-42.png">
2. Data preparation pipeline
- <img src="../data/image/2022-09-18-16-48-00.png">
  
  - omit ADASYN and RandomUnderSampler if balancing class weight instead
- feature scaling = MinMaxScaler
- feature engineering = SeasonSimilarity
  - kmeans clustering to represent different NBA eras
  - silhouette score for optimal # of clusters <img src="../data/image/2022-09-18-16-51-26.png">
- feature selection = L1 penalty with logisitc regression
  - to reduce training time
  - C = hyperparameter to tune
  - <img src="../data/image/2022-09-18-16-52-42.png">
3. Shortlist promising models
   - Quickly check performance of various models using 10-fold cross validation
   - <img src="../data/image/2022-09-18-16-53-52.png">
4. Hyperparameter tuning with RandomizedSearchCV
   - Tune top 5 models
   - Specify distribution of each hyperparameter (discrete uniform / continuous uniform / loguniform) <img src="../data/image/2022-09-18-16-57-50.png">
   - Use 10-fold cross validation and 100 iterations to search for best hyperparameters optimizing for Average Precision <img src="../data/image/2022-09-18-16-58-45.png">
5. Comparing performance on train set
   - Average precision <img src="../data/image/2022-09-18-16-59-21.png">
   - AUROC (too optimistic) <img src="../data/image/2022-09-18-16-59-40.png">
   - Precision-Recall curve <img src="../data/image/2022-09-18-17-00-06.png">
   - Coefficients for interpretability <img src="../data/image/2022-09-18-17-00-23.png">

# Step 3: Evaluation on test set
1. Load models and custom classes
2. Pick best model based on train set results
3. Evauate on test set

## Predicted Probabilities

## Precision-Recall Curve

## Average Precision (Area under PR Curve)

## Lift and gain chart

## Coefficients or Feature importance

## Confusion matrix

