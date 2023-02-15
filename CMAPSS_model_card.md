# Model Card

The models analysed in this card determine the remaining useful life (RUL) from 21 sensors relating to C-MAPSS output parameters.  The purpose of these models are to optimise hyperperameters for the models and assess improvement.


## Model Description

**Input:** Inputs to the model are simulated aircraft engine sensor data as described in the datasheet for C-MPASS file FD001, all numeric values.

**Output:** The model outputs remaining useful life (RUL) as a numeric value.

**Model Architecture:** The model includes:
1.  Baseline linear regression model
2.  Default k-nearest neighbour regression model
3.  Optimised k-nearest neighbour regression model (optimised for k)
4.  Default decision tree regression model
5.  Optimised decision tree regression model (optimised for max_depth, min_samples_split, min_impurity_decrease and ccp_alpha)
6.  Default random forest regression model
7.  Optimised random forest regression model (optimised for max_depth, min_samples_split, min_impurity_decrease and ccp_alpha)

### Hyperparameter optimisation
To optimise the k-nearest neighbour model I ran the model for k values between 1 and 19, and used the elbow method to select the best k value.

To optimise the the decision tree and random forest regression models I used a randomised parameter optimisation using scikit-learn's RandomizedSearchCV.  Optimising for the hyperparameters max_depth, min_samples_leaf, min_impurity_decrease and ccp_alpha.


## Performance

Root mean square error was used to assess the model performance.

The performance of the models are given below as a relative performance of RMSE against the baseline linear model.

![Model Performance Compared to a Baseline Linear Regression](/Images/test_performance.png)

The following plot shows the predicted RUL values for the test data for the baseline linear plot and the optimised random forest regression:

![Optimised random forest predictions](/Images/Opt_RF.png)

The optimal random forest hyperparameters were found to be:
-  max_depth = 9
-  min_samples_leaf = 21
-  min_impurity_decrease = 0.9
-  ccp_alpha = 0.95


## Limitations

The model is trained on CMPASS Jet Engine Simulated Data, use of the engine data from other sources may not be appropriate.
The model is trained on 3 operational settings, use of the model outside of these settings may not be appropriate.

## Trade-offs

I used the hyperparameter optimisation RandomizedSearchCV as it would be more efficient than an exhaustive search and I was time-limited for this project.  There may be a better hyperparameter optimisation available.
