# Taxi Order Forecasting with Time Series Modeling

This project was completed as part of a time series forecasting task for **Sweet Lift Taxi**, with the goal of predicting the number of hourly taxi orders **one hour into the future**. By building a predictive model, the company can better prepare for demand spikes and optimize driver availability.

---

## Dataset

The data comes from `/datasets/taxi.csv` and contains:

- `datetime`: Timestamp of each record (hourly frequency)
- `num_orders`: Number of taxi orders in that hour

---

## Objective

- Predict the number of taxi orders **one hour ahead**
- Achieve an RMSE (Root Mean Squared Error) of **no more than 48** on the test set

---

## ⚙️ Project Workflow

### 1. **Data Preprocessing**
- Resampled the data to hourly intervals
- Removed outliers (e.g., extremely high spikes above 60 orders)
- Ensured time index uniqueness and handled missing values

### 2. **Feature Engineering**
- Created lag features (`lag_1`, `lag_24`)
- Added rolling averages (`rolling_24`)
- Decomposed time series into `trend`, `seasonality`, and `residual` using `seasonal_decompose`
- Shifted the target column by one step ahead (`target = num_orders.shift(-1)`)

### 3. **Modeling**
- **Baseline**: Linear Regression  
- **Advanced Models**: Random Forest Regressor, LightGBM Regressor
- Evaluated each using RMSE on a 10% test split

---

## 📊 Results

| Model                    | RMSE     |
|-------------------------|----------|
| Linear Regression        | 27.77    |
| Random Forest Regressor | 21.88    |
| **LightGBM Regressor**  | **21.79** |

- LightGBM provided the best accuracy and efficiency
- Removing outliers improved model performance across the board
- Lag and rolling features were critical in modeling short-term patterns

---

## Conclusion

> The **LightGBM model** is the recommended solution for deployment, achieving a strong RMSE of **21.79**.  
> With clean data and thoughtfully engineered features, the model is capable of accurately forecasting hourly taxi demand — helping Sweet Lift optimize driver dispatch during peak and off-peak hours.

---

## 📁 File Structure

- `taxi.csv` – Source dataset
- `notebook.ipynb` – Main notebook with data processing, feature engineering, and modeling
- `README.md` – Project overview and documentation

---

## 📌 Notes

- All timestamp indices were confirmed to be unique
- Duplicate `num_orders` values were preserved due to natural seasonality
- No information leakage occurred — features were based only on past data relative to the prediction time

---

## 🚀 Future Improvements

- Hyperparameter tuning for LightGBM
- Incorporating external data (e.g., weather, holidays)
- Deploying the model as a forecasting API


