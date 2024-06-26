# Electricity Output Prediction using Wind Speed

## Table of Contents
- [Introduction](#introduction)
- [Project Goal](#project-goal)
- [Data Source](#data-source)
- [Setup](#setup)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Feature Engineering](#feature-engineering)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Prediction on New Data](#prediction-on-new-data)
- [Results](#results)
- [Conclusion](#conclusion)
- [Contact](#contact)
- [Discussion and Improvement](#discussion-and-improvement)

## Introduction
This project aims to develop a predictive model to forecast the electricity output (CF) of a wind farm based on wind speed data from various locations. The model's performance will be evaluated using the Mean Absolute Error (MAE) metric.

## Project Goal
The primary goal is to build a forecast model that accurately predicts the electricity output (CF) using historical wind speed data.

## Data Source
- **Train Sheet**: Historical data used for training the model.
  - Column B – "CF": Target variable representing the electricity output.
  - Columns C to DJ: Wind speed data from different locations.
- **Predict Sheet**: Data for prediction, containing wind speed features.

## Setup
### Prerequisites
```
Python 3.6 or higher
Jupyter Notebook
numpy==
autogluon.tabular==1.1.1
keras==2.12.0
tensorflow==2.10.1
```

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/Maggie-prog/my-cf-electricity-output-prediction-challange.git
   cd my-cf-electricity-output-prediction-challange

## Exploratory Data Analysis
### Univariate Analysis
- **Numerical Variable Distribution**
    1. Wind Speed Distribution Across 112 Locations:
        - The wind speed distributions across the 112 different locations approximately follow normal or uniform distributions, with no apparent outliers.
    2. Wind Speed Distribution Across All Time Points:
        - The wind speed distributions across all time points also approximately follow normal or uniform distributions, with no apparent outliers.
    3. Central Tendency:
        - The mean and median of the wind speed data are similar, indicating a symmetric distribution.
    4. Decision:
        - Based on these distributions, we extracted the minimum, maximum, and several key percentiles at each time point to represent the characteristics of the wind speed distribution effectively.

- **Categorical Variable Cardinality**
    1. Categorization Based on Time Points: The data is categorized into various time-related features such as year, month, day, season, weekday, and day/night.
    2. The proportion of data points in autumn is higher compared to winter and summer. The data points are evenly distributed between weekdays and weekends. Measurements taken at different times of the day are also uniformly distributed.

<div align="center">
  <img src="https://github.com/Maggie-prog/my-predictive-modeling-challenge/blob/master/fig/countplot.png" width="100%">
</div>

### Bivariate analysis
- **Numerical analysis - Correlation**
    1. Our mean wind speed is most correlated with the target value at 0.88, and several other aggregate values also have correlations above 0.7. Therefore, we infer that the distribution of wind speeds from different regions at previous time points is related to the characteristics of the wind speed at the next time point. To avoid overfitting, we can use summary statistics of the wind speeds instead of the original features.

    2. We also checked the wind speeds from different regions, as well as our aggregate wind speed values, for their Pearson and Spearman correlations with the target value. We found that the wind speeds from over 50% of the regions are strongly correlated with the target value.

- **Categorical analysis**

  Based on ANOVA tests, t-tests, and density curves by subgroup, it is evident that there is a strong correlation between seasons and electricity output. Additionally, there is a noticeable relationship between day/night cycles and electricity output.
  
<div align="center">
  <img src="https://github.com/Maggie-prog/my-predictive-modeling-challenge/blob/master/fig/distribution_day_night.png" width="100%">
</div>

- **Dual plot**

    As we can see, MEAN_WS_smooth, P95_WS_smooth, P5_WS_smooth, and electricity output are strongly correlated.

    The analysis reveals that:

    Wind speeds from previous time points influence the current wind speed.
    The current wind speed is strongly correlated with electricity output.
    Thus, it can be concluded that wind speeds from past time points indirectly affect the current electricity output.

<div align="center">
  <img src="https://github.com/Maggie-prog/my-predictive-modeling-challenge/blob/master/fig/Time_Series.png" width="100%">
</div>

### Multivariate Analysis
Based on the coefficients from OLS regression and the feature importance from the decision tree, we explored both the linear and nonlinear relationships between features and the target value. This analysis allowed us to perform an initial feature selection.

## Model Training and Evaluation

### Strategy A（Autogluton Weighted Ensembled L2 regression model）
We use the current time point's wind speed, as well as features such as season and daylight, to predict the electricity output at the current time, without considering the temporal correlation between different time points.

### Strategy B（LSTM， Multivariate time series forecasting model）
We use the wind speed information from previous time points (lagging features) to predict the current electricity output, taking into account the temporal correlation between different time points.

## Prediction on New Data
- Scaling the new data using the previously fitted scaler.
- Making predictions on the new data.
- Saving the predictions to an Excel file.

## Results
The Excel file Wind_data_submission.xlsx and submission_LSTM.xlsx contains the predicted electricity output for the new data.

## Conclusion
This project demonstrates the application of machine learning techniques to predict electricity output based on wind speed data. The model's performance, evaluated using MAE, provides insights into its accuracy and potential improvements for future work.

## Contact
For any questions or inquiries, please contact siqizhong322@gmail.com

## Discussion and Improvement
1. 可以花更多时间做更细致的feature selection、更精细的hyperparameter optimization
2. predictiion interval：可以将目前loss function的MSE改为quantile regression loss
3. not only point estimate， also precision and variability estimation
