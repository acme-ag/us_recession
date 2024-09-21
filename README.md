# Predicting US recession probabilities using Machine learning models

## Overview

This project aims to explore and predict the likelihood of a recession in the United States by leveraging a comprehensive dataset of key economic indicators. 

The project was inspired by recent discussions within economic communities and social media platforms, particularly Reddit, where concerns about unemployment, economic slowdown, and potential recession were widely debated during 2024. These discussions were further fueled by reports suggesting that the U.S. might already be experiencing a “hidden recession.” (remember "Sahm's rule" that was the buzz recently?) Well. this raised curiosity about -- whether it is possible with the available economic data gather/generate insights or predict the probability of a recession in the near future. 

**Disclaimer:** of course I know it is very hard (if possible at all), since the recession are very rare events (and that is a major pain for ML) and are very different by nature. The most recent one was caused by "black swan" -- pandemy, the one before that -- by real estates market bubble (although some were able to predict that one), and before that was recession caused by dotcom crisis, oil market crisis and so on. But it was interesting to combine dataset and apply some techniques and see what level of precision can be achieved.

## Purpose

The primary objective of this project is to combine historical economic data from various reputable sources, build machine learning models, and assess their performance in predicting the likelihood of a U.S. recession over the next 10 months. By analyzing key economic indicators and employing advanced modeling techniques, the project aims to quantify recession risks and evaluate the accuracy of different models.

## Data collection

The dataset for this project spans from 1948 to 2024 and combines a variety of economic indicators from multiple reliable sources such as the Bureau of Census, the Federal Reserve, and the World Trade Organization (WTO). However, gathering and processing the data presented several challenges, as the data was often provided in different formats and sometimes contradictory across sources. These issues required extensive data cleaning, validation, and harmonization to ensure consistency. Key challenges included:

-	Inconsistent formats: data from different sources, such as CSV files, PDFs, and web-based tables, were not always structured uniformly. This required significant effort to standardize formats and ensure compatibility for analysis.
-	Conflicting data: in some cases, data from one official source would not match the figures provided by another source, even when referring to the same economic indicator. These discrepancies had to be resolved through cross-referencing and, where possible, using the most credible or comprehensive dataset.
-	Missing data: for certain periods, particularly in older datasets, data was missing or incomplete. In these instances, indirect methods, such as interpolation and estimation from related indicators, were used to infer the missing values, ensuring the dataset maintained continuity across the entire time range.
-	Data cleaning: extensive preprocessing was necessary to handle outliers, smooth noisy data, and fill in missing values where appropriate. This process also involved aligning timeframes and adjusting for seasonality and inflation in some of the economic indicators.

### Key indicators collected include:

- GDP: real GDP and real GDP growth rate, sourced from the Federal Reserve Economic Data. 
  - real GDP (https://fred.stlouisfed.org/series/GDPC1)
  - real GDP rate (https://fred.stlouisfed.org/series/A191RL1Q225SBEA)
- Recession dates: obtained from FRED.
  - https://fred.stlouisfed.org/series/USREC
- Unemployment rates: data from the Bureau of Labor statistics.
  - https://data.bls.gov/pdq/SurveyOutputServlet
- Industrial production: sourced from the Federal Reserve’s Industrial Production and Capacity Utilization reports.
  - https://www.federalreserve.gov/releases/g17/current/default.htm
- Stock market data: Dow Jones Industrial and S&P500 performance from S&P Global.
  - https://www.spglobal.com/spdji/en/web-data-downloads/reports/dja-performance-report-daily.xls%3Fforce_download%3Dtrue&ved=2ahUKEwjYyZTEp9KHAxVaBDQIHS1pDXU4ChAWegQICBAB&usg=AOvVaw0HHk557jTY0ImxjKP4DqAc
- Yield curve data: 3-month Treasury bill yield data from FRED.
  - https://fred.stlouisfed.org/series/TB3MS
- Housing market data: housing starts and house price indices from the U.S. Census Bureau and Shiller data (Irrational Exuberance, by R. Shiller).
  - https://fred.stlouisfed.org/series/HOUSTNF
  - http://demographia.com/db-hstarts.pdf
  - https://www.census.gov/construction/nrc/historical_data/index.html
  - https://www.census.gov/construction/nrc/data/series.html
  - https://shillerdata.com
  - https://fred.stlouisfed.org/series/USSTHPI
  - https://observationsandnotes.blogspot.com/2011/06/us-housing-prices-since-1900.html
- Credit data: consumer loans and real estate loan data from FRED.
  - https://fred.stlouisfed.org/series/CONSUMER
  - https://fred.stlouisfed.org/series/CONSUMERNSA
  - https://fred.stlouisfed.org/series/REALLNNSA
- Consumer price Index (CPI) and Inflation rates: data on CPI and historical inflation rates from FRED and rate inflation.
  - https://fred.stlouisfed.org/series/CPIAUCSL
  - https://www.usinflationcalculator.com/inflation/consumer-price-index-and-annual-percent-changes-from-1913-to-2008/
  - https://www.rateinflation.com/inflation-rate/usa-historical-inflation-rate/
- Global economic data: data on global trade and economic conditions sourced from the WTO.
  - https://www.wto.org/english/res_e/statis_e/trade_evolution_e/evolution_trade_wto_e.htm

Of course there can be added more inicators and I'm working on that.

## Methodology

The project applies a combination of time-series analysis and machine learning to model and predict recession probabilities. 

Initially, a Vector Auto-regression (VAR) model was used to generate reliable data forecasts for the period between March 2024 and January 2025. Indicators such as unemployment rates and inflation showed a close match between predicted and actual data, validating the accuracy of the VAR model.

The next step involved using the forecasted data as input to predict the probability of a recession in the next 10 months, utilizing the following machine learning models:

- Logistic regression: this model was used as a baseline model to establish performance benchmarks.
- Random Forest classifier: implemented to improve precision and recall, particularly for predicting recession periods.
- XGBoost: applied to further enhance model accuracy and improve recession detection using resampling techniques like SMOTE.
- Support Vector Machines (SVM): explored for their effectiveness in handling complex, non-linear relationships in the data.
- Ensemble techniques: combined various models to improve overall performance and robustness in predicting recessions.

## Metrics and evaluation

To evaluate the performance of the models, several key metrics were employed to capture different aspects of predictive quality:

- Accuracy: measures the overall percentage of correct predictions (both recession, 1, and non-recession, 0).
- Precision: evaluates the proportion of true positive predictions (correctly predicted recessions) relative to all predicted recessions.
- Recall: measures the ability of the model to capture actual recession periods (the proportion of true recessions correctly identified).
- F1-score: the harmonic mean of precision and recall, providing a balanced measure of model performance.
- Area Under the ROC Curve (AUC-ROC): used to evaluate the model’s ability to distinguish between recession and non-recession periods. The AUC score provides insight into how well the model differentiates between classes, with a higher score indicating better performance.

These metrics crucial in comparing the different models, with XGBoost emerging as the best performer (or one of...), achieving an AUC score of 0.912 and an accuracy of 85%, along with a recall of 55% for recession periods, signifying its capability to capture important economic downturns while maintaining high precision for non-recession periods.

## Results and insights

Preliminary results indicate that the Random Forest and XGBoost models perform well in predicting recession probabilities, with the Random Forest model demonstrating strong accuracy for non-recession periods and the XGBoost model offering improved recall for recessions. Feature importance analysis revealed that GDP growth rates, consumer loans, and CPI fluctuations are among the most critical factors influencing recession predictions.

## Roadmap

1.	Data collection and preprocessing:
	- Compile historical data from reliable economic sources.
	- Perform feature engineering and clean the dataset to ensure consistency across time periods.
2.	Time-Series forecasting:
	- Apply the VAR model to forecast key economic indicators for the next 10 months (April 2024 to Jan 2025).
	- Measure its performance against ARIMA model (on a certain indicators) 
	- Validate the forecasted data against real-world observations.
3.	Machine learning modeling:
	- Train logistic regression, random forest, XGBoost, and SVM models using the forecasted data.
	- Evaluate models based on precision, recall, F1-score, and accuracy.
	- Utilize cross-validation and AUC-ROC metrics to ensure robustness.
4.	Feature importance and interpretability:
	- Analyze feature importance to identify key economic indicators driving recession predictions.
	- Interpret model predictions in the context of real-world economic conditions.
5.	Final evaluation and predictions:
	- Use ensemble methods to combine model outputs and generate a final prediction for the probability of a U.S. recession.
	- Assess the model’s performance in predicting recession probabilities over the next 10 months.

## Conclusion

This project presents a comprehensive approach to measuring and predicting U.S. recession probabilities using advanced machine learning techniques and a diverse set of economic indicators. Throughout the analysis, several models were tested and evaluated, with **XGBoost** and the **Ensemble model** standing out as the most effective in predicting the probability of a recession.

After thorough experimentation, XGBoost emerged as one of the top-performing models, achieving a cross-validation AUC score of **0.912**. It demonstrated strong performance in distinguishing between recession and non-recession periods, achieving an overall accuracy of **85%**. Notably, XGBoost achieved a recall of **55%** for recession periods, which indicates that it was able to correctly capture more than half of the actual recession events, a significant improvement over the baseline Logistic Regression model.

The **Logistic regrssion** model, while offering a solid baseline, struggled to accurately capture recession periods. With an AUC score of 0.615 and an accuracy of 57%, it highlighted the need for more complex models to improve predictive accuracy, especially for rare events like recessions.

The **Random forest** classifier also performed well, particularly in terms of precision for predicting non-recession periods, achieving an AUC score of 0.812. However, it had limitations in recalling recession events, capturing only 25% of actual recession periods. This trade-off between precision and recall made Random Forest more suitable for predicting stable (non-recession) periods rather than rare recessions.

The **SVM** model provided similar challenges, with an AUC score of 0.600 and a recall of 65% for recessions, but precision suffered significantly, making it less reliable overall.

### Ensemble model:

The **Ensemble method**, which combined the strengths of multiple models (Logistic regression, SVM, Random forest, and XGBoost) using a soft voting classifier, improved performance across several metrics. The ensemble approach achieved an AUC score of **0.738** and balanced both precision and recall for recession periods, capturing **55%** of recessions. Although it did not outperform XGBoost in all areas, it provided a more stable prediction by leveraging the strengths of individual models.

These results suggest that, based on the indicators used, **XGBoost** provides the most reliable predictions for U.S. recession probabilities, offering both high accuracy and reasonable recall for recession periods. However, the Ensemble model offers a more balanced approach and can be considered as an alternative when greater stability and consistency across predictions are needed.

The forecasted economic data for april to september 2024 aligned closely with real-world trends, reinforcing the reliability of the models. The ability to predict recession probabilities with such precision can provide valuable insights for policymakers, economists, and financial analysts, offering them the tools to anticipate and prepare for economic downturns.

While the models performed robustly, there are areas for further improvement. Future work could focus on incorporating additional macroeconomic features, refining feature engineering techniques, or adjusting decision thresholds to further enhance recall for recession periods. These improvements could lead to even more accurate and actionable recession forecasts, aiding decision-making in economic policy and financial markets.
