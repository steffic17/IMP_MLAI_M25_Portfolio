# Predict the Remaining Useful Life of a Jet Engine


## Summary
This project uses a CMPASS Jet Engine Simulated Data Set to determine the remaining useful life (RUL)of a jet engine based on the simulated output from 21 simulated engine sensors.  This project was completed as the final portfolio project for the Imperial College Professional Certificate in Machine Learning & Artificial Intelligence in February 2023.

## Data Used
The data used comes from the CMPASS Jet Engine Simulated Data dataset available from NASA, "NASA's Open Data Portal" [2].  For this project I have only used the FD001 data.

### Assessment of sensors
![Sensor readings for training data](/Images/sensors.png)

Image of sensor readings from training data

- Sensors 1, 5, 10, 16, 18 & 19 all show flat line trends to RUL, these can be excluded.
- Sensor 6 shows spikes that appear unrelated to RUL, this can also be excluded.
- Sensors 2, 3, 4, 8, 11, 13, 15 and 17 show a trend to increase as RUL decreases.
- Sensors 7, 12, 20 and 21 show a trend to decrease as RUL decreases.
- Sensors 9 & 14 show a trend to decrease/increase as RUL descreases depending on the engine unit.

Note that the sensors do not show a linear relationship to RUL.  Instead there appeard to be a period of constant reading followed by a 'degrading' period where the sensor data diverges.

### Remaining Useful Life (RUL)
![RUL distribution](/Images/RUL_distribution.png)

The engines in the training data have between 50 and 350 cycles of RUL remaining, with a peak of engine units having around 200 cycles of RUL.

## MODEL 
I have used a number of machine learning models to predict RUL.  I have used the following models:
1.  Baseline linear regression model
2.  Default k-nearest neighbour regression model
3.  Optimised k-nearest neighbour regression model (optimised for k)
4.  Default decision tree regression model
5.  Optimised decision tree regression model (optimised for max_depth, min_samples_split, min_impurity_decrease and ccp_alpha)
6.  Default random forest regression model
7.  Optimised random forest regression model (optimised for max_depth, min_samples_split, min_impurity_decrease and ccp_alpha)A summary of the model you’re using and why you chose it. 

I chose these models as they are commonly used machine learning methods and I wanted to investigate the applicability of a range of models.

## HYPERPARAMETER OPTIMSATION
When optimising the hyperparameters for the models I optimised the following:
-  **k-nearest neighbour regression model** optimised for the number of neighbours considered in the model, k.
-  **Decision tree regression model** optimised for max_depth, min_samples_leaf, min_impurity_decrease and ccp_alpha
-  **Random forest regression model** optimised for max_depth, min_samples_leaf, min_impurity_decrease and ccp_alpha)

In the case of the k-nearest neighbour model I ran the model for k values 1,3,5,7,9,11,13,15,17,19 and used the elbow method to select the best k value.  In this case the optimum k value was 5, which is also the default model value.

For the decision tree and random forest regression models I used a randomised parameter optimisation using scikit-learn's RandomizedSearchCV.  I chose this method as it would be more efficient than an exhaustive search and I was time-limited for this project.
I chose hyperparameters in the following ranges:
-  **max_depth** none to depth 40, the default value was set to none
-  **min_samples_leaf** between 1 and 101, the default value was set to 1
-  **min_impurity_decrease** between 0 and 10, the default value was 0
-  **ccp_alpha** between 0 and 2, the default value was 0


## RESULTS
The first plot gives the performance of the training and test root mean square errors for all the machine learning methods.  The second plot gives RMSE error relative to the linear baseline model.
![RMSE for models, training & test](/Images/performance.png)

![Relative RMSE for models, test only](/Images/test_performance.png)

These are some key points to note:
1. the baseline linear regression is difficult to improve upon
2. the default KNN regression is also the optimised KNN regression
3. the default decision tree regression is overfitting the data (fits training data perfectly, but predicts poorly on test data)
4. the default random forest regression also overfits the training data, but not to the same degree as the decision tree regression.
5. the optimised random forest regression model is the only model that improves upon the baseline linear regression and with a modest 4.8% improvement.
6. it is unusual that the baseline linear test RMSE is lower than the training RMSE. It is supposed that this is due to the nature of the sensor data remaining constant and then entering a 'degrading' period.  Since the test data is mostly from this degrading period the model fits better as it approaches engine failure.

The optimal random forest hyperparameters were found to be:
-  max_depth = 9
-  min_samples_leaf = 21
-  min_impurity_decrease = 0.9
-  ccp_alpha = 0.95

The following plot shows the predicted RUL against the actual RUL for the linear baseline model and the optimised random forest model.

![Optimised random forest predictions](/Images/Opt_RF.png)


## CONTACT DETAILS
Stef Church stef.church@engineeringtheblue.com



[1]  A Saxena, K Goebel, D Simon, N Eklund, "Propagation Modeling for Aircraft Engine Run-to-Failure Simulation", 2008
[2]  NASA, "NASA's Open Data Portal", https://data.nasa.gov/Aerospace/CMAPSS-Jet-Engine-Simulated-Data/ff5v-kuh6, last accessed on February 2023.