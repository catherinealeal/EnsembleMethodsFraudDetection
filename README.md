# Fraud Detection via Ensemble Methods

## Goals 
- Explore two ensemble methods: AdaBoost and Random Forests 
- Use key performance indicators (KPIs) appropriate for highly skewed data 
- Characterize model performance with ROC curves

## Data Collection 

This dataset contains transactions made by credit cards in September 2013 by european cardholders. The dataset is highly unbalanced, the positive class (frauds) account for 0.17% of all transactions. The data is already PCA transformed. 

[Dataset](https://www.cs.utexas.edu/~chaney/cc.csv)

## Partition Data for Cross Validation

Using a stratified k-fold to preserve the class balance so our target class is not underrepresented in any k-fold selection.

Using k = 3

- d_train_df_X : where the key is the fold number, and the value is the attribute training dataframe at that fold
- d_test_df_X : where the key is the fold number, and the value is the attribute test dataframe at that fold
- d_train_s_y : where the key is the fold number, and the value is the target training series at that fold
- d_train_s_y : where the key is the fold number, and the value is the target test series at that fold

## Part 1: AdaBoost 

Loop over the k folds using the dictionaries from above, and for each fold calculate the accuracy, TPR, the PPV, and the FPR. Plot the ROC curve for each fold.

AdaBoost parameters: 
- n_estimators = 25 
- random_state = 23

<img width="485" alt="Screenshot 2024-01-11 at 2 24 52 PM" src="https://github.com/catherinealeal/EnsembleMethodsFraudDetection/assets/100166102/460ea277-18bb-4697-80b6-be5b10104711">

- The min, mean, and max true positive rate (TPR) are: 0.62, 0.65, and 0.71
- The min, mean, and max positive predictive value (PPV) are: 0.75, 0.79, and 0.82
- The min, mean, and max accuracy (ACC) are: 1.00, 1.00, and 1.00

## Part 2: Random Forests 

Loop over the k folds using the dictionaries from above, and for each fold calculate the accuracy, TPR, the PPV, and the FPR. Plot the ROC curve for each fold.

Random Forest Parameters 
- criterion = 'entropy'
- max_features = 'sqrt'
- random_state = 23

<img width="479" alt="Screenshot 2024-01-11 at 2 26 40 PM" src="https://github.com/catherinealeal/EnsembleMethodsFraudDetection/assets/100166102/3dab377f-5459-4cbe-9d77-34f239e1c218">

- The min, mean, and max true positive rate (TPR) are: 0.00, 0.24, and 0.71
- The min, mean, and max positive predictive value (PPV) are: 0.00, 0.27, and 0.80
- The min, mean, and max accuracy (ACC) are: 1.00, 1.00, and 1.00

## Part 3: Calculate the Cost of Fraud

Above, the predictions in the 3rd fold were saved into variables `y_hat_ab` and `y_hat_rf` for the AdaBoost and RandomForest models respectively. 

Calculate how much money will be saved by deploying either of these fraud algorithms to the real-time payment processing system, asssuming that there is not a currently deployed fraud detection algorithm.  

Rules: 
- For every fraudulent transaction that is not predicted as fraudulent, the bank looses twice the value of the transaction.  
- If a charge is predicted as fradulent, but wasn't, it costs the bank a flat fee of €3 in customer service support to communicate with the customer, and mark the possible fraud as a normal transaction.

Savings with AdaBoost: $6314.20

Savings with Random Forests: $7601.00

## Conclusion 

The bank will save about $7601 if they deploy the Random Forest algorithm to detect fraud.

### View full notebook [here](https://github.com/catherinealeal/EnsembleMethodsFraudDetection/blob/main/EnsembleMethodsFraudDetection.ipynb)
