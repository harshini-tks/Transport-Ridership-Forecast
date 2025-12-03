PUBLIC TRANSPORT RIDERSHIP FORECASTING
INSIGHTS


INTRODUCTION

Public transport ridership forecasting is essential for efficient service planning, vehicle allocation, peak-hour management, and overall operational decision-making.
This project aims to analyze historical passenger journeys across multiple service types and build a short-term forecasting model capable of predicting ridership for the next 14 days.
The primary goals of this project are:
Perform Exploratory Data Analysis (EDA) to uncover key trends and seasonality
Understand service-level behaviors and long-term ridership changes
Build an interpretable machine learning model for forecasting
Evaluate model performance using standard metrics
Produce actionable insights for operational planning

INSIGHT 1:
Strong Weekday–Weekend Pattern
  
We found the Average Total Passengers

Weekdays=36,818
Weekends=20,920

All service types show significantly lower ridership during weekends.
School drops by 67%
Peak Service drops by 66%
Local Route drops by 51%
Rapid Route drops by 39%

Conclusion:
On weekdays, public transport is used much more because of work and school travel. On weekends, usage falls a lot across all services, especially school and peak services. This shows clear weekly patterns in how people travel.

INSIGHT 2:
COVID-19 Caused a Major Ridership Collapse, Recovery Still Incomplete

Year
2019    44471.625000
2020    26327.237705
2021    25499.750685
2022    29679.000000
2023    37112.791781
2024    37979.183150

Interpretation
Ridership fell ~40–43% during the pandemic (2020–2021).
2024 ridership is still ~15% lower than 2019 levels.
Slow but steady recovery is seen from 2022–2024.

Conclusion:
The number of passengers was highest before COVID, then fell a lot in 2020–2021, and although it has been increasing again, it is still lower than 2019 levels. This shows slow recovery over the years.

INSIGHT 3:
Rapid Route is the Backbone of the Transport Network
Interpretation
Rapid Route consistently carries the highest share (~40%) every year.
Light Rail usage is growing steadily, increasing by ~2% since 2019.
Local Route remains stable around ~30%.
Conclusion:

Rapid Route is the most-used service across all years. Local Route and Light Rail also have steady usage, while School and Peak Services make up only a small part of total travel. The share of each service stays mostly stable over time.

INSIGHT 4:
School Service is Highly Seasonal

Interpretation
Ridership strongly aligns with school calendars.
Sharp declines occur during:
Winter vacation (Dec–Jan)
Term breaks

Conclusion:
School ridership is highest during regular school months and becomes very low during holidays. This shows clear seasonal patterns where school breaks heavily reduce passenger numbers.


MODEL - RANDOM FOREST

I selected the Random Forest Regressor because it works extremely well for forecasting multiple correlated time-series when combined with lag and calendar features. Unlike ARIMA or Prophet, Random Forest:
Can predict all service types together (multi-output forecasting)
Learns non-linear patterns such as weekday/weekend differences, school seasons, and holiday dips
Is robust to noise and outliers, which are common in transport data
Makes no strict assumptions about trend or seasonality
Provides feature importance, making the model explainable
Most importantly, Random Forest outperformed the baseline model, reducing MAE by 35–47%, proving it is a suitable and accurate choice.
Outperformed Naive Baseline by 35–47%

Hyperparameter 

n_estimators=300
max_depth=12
min_samples_leaf=5
random_state=42
n_jobs=-1

Here is why each parameter was chosen:

n_estimators = 300

Number of trees in the forest.
More trees → more stable predictions
After ~300 trees, performance stops significantly improving
Balanced between accuracy and computation time

max_depth = 12

Maximum depth of each decision tree.
Deeper trees capture more patterns but may overfit

Depth=12 

gives enough complexity to learn:
weekday/weekend patterns
lags
seasonal effects
Prevents trees from becoming too complex

min_samples_leaf = 5

Minimum samples required at a leaf node.
Ensures leaves are not created from very small, noisy samples
Smooths predictions
Prevents extreme forecast spikes

random_state = 42

Ensures reproducibility.
Same model → same output every time
This is critical for reporting and evaluation

n_jobs = -1

Use all CPU cores.
Faster training
Especially useful with large feature sets (lags + calendar features)


Conclusion:

It models multiple correlated services at once
It handles nonlinear patterns, spikes, holidays, school terms, and weekly cycles
It is resistant to noise and outliers
It is easy to interpret for decision-makers
It significantly outperformed the baseline model
It produces smooth, realistic short-term forecasts
Given the complexity of the ridership data and the forecasting requirements, Random Forest was the most appropriate and effective choice for this project.
