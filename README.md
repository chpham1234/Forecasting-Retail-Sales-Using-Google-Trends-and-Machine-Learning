# Experiment Design and Model Application 

## Dataset URL: https://www.kaggle.com/olistbr/brazilian-ecommerce

The scope of the experiment consisted of using the Olist dataset to generate daily forecasts spanning a period of 14 days in the state of Sao Paolo. The SARIMA and FBProphet models were trained on historical sales data beginning on July 7th, 2017 for predictions made between December 1st, 2017 and December, 14th, 2017. 

The optimal parameters used by the SARIMA model were determined using a grid search technique whereas the FBProphet model did not contain hyperparameters. The start date of the training dataset used by the XGBoost and LSTM models was the same as in the SARIMA and FBProphet models. The XGBoost and LSTM models additionally contained a validation set used for hyperparameter tuning that began on November 11th, 2017 running until December 1st, 2017 when the first prediction is made. The size of the validation set was determined based on a heuristic trial approach by testing out different sizes. In total, there were six demand forecasting models used to generate forecasts, aggregated at a daily level by product category and each model was run for seven different product categories. 

The top seven product categories demanded on Olist as measured by the all time number of orders received were selected. A Python Jupyter notebook was developed for each model, totalling six notebooks. The models implemented were SARIMA, FBProphet, univariate XGBoost, multivariate XGBoost, univariate LSTM and multivariate LSTM. The univariate version of the XGBoost and LSTM models utilizes only historical sales data to generate a forecast and the multivariate version includes Google Trends series as an addition. This setup emphasizes the analysis on potential forecast improvements as a result of the inclusion of Google Trends in the XGBoost and LSTM models. 

Each notebook utilizes a configuration file containing arguments that tailor the processing of data according to the requirements of the model at hand.

The configuration file contains the file directories used from the Olist dataset and expects a list of product category names to be passed for which data processing operations are conducted on. Depending on the model, the values within the configuration file may vary. For example, in the case of an XGBoost multivariate model, the window_size argument was used to specify the number of historical lags to be generated and used in making a prediction for day t+1. Similarly, the add_date_features arguments if set to ‘true’ will trigger the extraction of date features used by the XGBoost model as opposed to the raw date format that other models like SARIMA work with. 

This approach was used to ensure traceability and consistency of processing rules used to run each model in addition to providing the flexibility to extend the configuration according to needs in future projects. Each time a model was run the performance metrics and parameters used by each model and product category were logged using MLFlow. In the case of SARIMA and FBProphet, performance was logged only for the testing set. Whereas, for XGBoost and LSTM models performance metrics were logged for the validation and testing set to obtain a better visibility on model learning and forecast error. 

The Google Trends series downloaded from the official user interface were only used by the XGBoost and LSTM multivariate models. Therefore, the configuration file does not expect arguments specific to Google Trends series and massaging of data format required. Instead, the integration of the Google Trends series was addressed directly in the Python Jupyter notebooks for the models that used this information.
