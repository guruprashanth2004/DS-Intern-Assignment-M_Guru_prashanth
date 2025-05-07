# Smart Factory Energy Prediction Challenge

## Problem Overview

SmartManufacture Inc. has deployed a sensor network in a manufacturing facility to monitor environmental conditions and energy usage. The goal is to build a machine learning model that **accurately predicts equipment energy consumption** using sensor and environmental data, helping managers optimize operations and reduce energy costs.


## Dataset Summary

- **Target Variable**: `equipment_energy_consumption` (in Wh)
- **Features**: 
  - Indoor zone temperatures and humidities from 9 zones
  - External weather conditions (e.g., temperature, humidity, wind speed)
  - Lighting energy
  - Random variables: `random_variable1`, `random_variable2`
  - Timestamps


## Exploratory Data Analysis (EDA)

- The dataset showed:
  - Right-skewed distribution of equipment energy
  - Strong correlations with temperature and humidity in **Zones 1–4**
  - Meaningful seasonal/hourly patterns tied to the `timestamp`
  - `random_variable1` and `random_variable2` showed negligible correlation with energy consumption and were excluded


## Data Preprocessing

- Converted `timestamp` to datetime and extracted `hour`, `dayofweek`
- Converted all columns (except timestamp) to numeric
- Filled missing values using forward and backward fill
- Standardized feature scales using `StandardScaler`


## Model Development

- **Model Used**: `RandomForestRegressor` (robust to non-linearities and outliers)
- **Training/Test Split**: 80/20
- **Cross-validation**: Performed using holdout set

### Evaluation Metrics:

| Metric       | Value      |
|--------------|------------|
| RMSE         | 174.55   |
| MAE          |  70.74   |
| R² Score     | 0.1018   |

- These scores show strong predictive performance on unseen data


## Feature Importance

Top 10 features influencing equipment energy consumption:

1. `hour`
2. `zone5_humidity`
3. `atmospheric_pressure`
4. `zone6_humidity`
5. `zone8_temperature`
6. `zone3_temperature`
7. `zone7_humidity`
8. `zone9_humidity`
9. `zone6_temperature`
10. `dew_point`


## Key Insights & Recommendations

1. **Time-Based Energy Patterns**
   - `hour` is the most influential variable.
   -  *Energy usage follows a predictable daily cycle. Use this to schedule high-energy operations during off-peak hours.*

2. **Humidity Monitoring**
   - `zone5_humidity`, `zone6_humidity`, `zone7_humidity`, `zone9_humidity` are critical.
   -  *Install dehumidifiers or optimize ventilation in these zones to control energy spikes.*

3. **Pressure & Dew Point Effects**
   - `atmospheric_pressure` and `dew_point` suggest external weather affects internal energy use.
   -  *Use weather forecasts to pre-adjust HVAC and reduce unnecessary loads.*

4. **Zone-Specific Climate Control**
   - `zone6_temperature`, `zone8_temperature`, and `zone3_temperature` are key drivers.
   -  *Implement zone-level climate control instead of factory-wide systems.*

5. **Predictive Scheduling**
   - Combine time (`hour`) and environmental data to build a dynamic energy usage schedule.
   -  *Automate equipment usage based on low energy cost windows.*


## Conclusion

A robust machine learning model was developed that predicts equipment energy consumption with high accuracy. With actionable insights and predictive capabilities, SmartManufacture Inc. can now offer its client an intelligent energy management solution that drives cost savings and environmental sustainability.

---

##  Files Provided

- `smart_factory_energy_model.ipynb`: Full implementation code
- `data.csv`: Dataset used for training/testing
- `smart_factory_report.md`: This report
