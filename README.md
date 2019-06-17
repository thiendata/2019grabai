# Submission for Grab AI Traffic Mgmt  time-series regression problem.
Environment tested
* Google Collab

To run 
* Read data into variable 'dataset' dataframe
* Run code till the core model running
* Final Predictions are stored in 'Preds['gradientBoostRegressor4']' dictionary (dictionary as still testing various models)

Assumptions
* Final dataset would be similar (with demand too). Not using test demand for any purpose except RMSE calculation
* Took the last 5 records as test data (not T+1, ... T+5)
* Took only records within last 14 days of first test data as per required
* Some data is really sparse (only 1-2 records) and predictions would be hardcoded

# What work
* Surprisingly GradientBoostingRegressor was the best
* Hyperparameter tuning using GridSearchCV also found max-depth=1 with estimator=40 reduce the RMSE slightly (surprisingly again, increasing estimator didn't help even though GBR should like overfitting)
* RandomForest and XGBoost was comparable but dropped since results are too similar

# What didn't
Too many (used out-of-box) but just to list 
* Auto-arima, TBATS, RNN (though didn't run through enough epoch), Facebook Prophet, LGB
* Feature engineering
** day of week field (though it was noted two of 7 days had lesser demand
** historical timestamp demand
** Getting T-1 previous demand, neighbor demand, median of demand, filling "missing" data with demand = 0, historical 0 demand timestamps
(thought there was missing data until saw the FAQ mentioned missing data -> demand=0)
