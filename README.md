# Used Car Price Prediction (Serbia)

> Note: This is my first project in machine learning and data science. The main goal was to learn and practice the full workflow (web scraping, data cleaning, exploratory analysis, and model development), not to build a production-ready or perfectly tuned model.

A project that predicts used car prices based on data scraped from polovniautomobili.com, the largest used-car marketplace in Serbia.

## Project Structure

- scraping.ipynb: scrapes car listings (price, age, mileage, engine size, power, fuel type, transmission, body type) and saves them to cars.csv
- modeling.ipynb: data cleaning, outlier detection, exploratory data analysis, and iterative development of a linear regression model
- requirements.txt: Python dependencies

## Data

Around 1700 listings scraped directly from the site. The full dataset is not included in this repo; run scraping.ipynb to regenerate it.

| Column | Description |
|---|---|
| cena | Price (EUR) |
| starost | Age (years) |
| karoserija | Body type |
| kubikaza | Engine size (cm3) |
| gorivo | Fuel type |
| kilometraza | Mileage (km) |
| snaga_kw / snaga_ks | Power (kW / HP) |
| menjac | Transmission |
| broj_vrata / broj_sedista | Doors / seats |

## Approach

1. Data cleaning. Handled missing values during scraping, grouped rare categories, removed data-entry errors and extreme outliers.
2. EDA. Correlation analysis, distribution checks, outlier inspection.
3. Baseline model. Linear regression on raw price; revealed heteroscedasticity and impossible negative predictions.
4. Log-transformed model. Resolved both issues, substantially improving MAPE (99% to 36%).
5. Ridge regression. Tested for overfitting; no meaningful improvement (optimal alpha close to 0).
6. Outlier filtering. Removing high-power cars lowered RMSE but worsened MAPE, showing that a single metric can be misleading.

## Final Model

Log-transformed linear regression (lre_log).

- R-squared (test): approximately 0.81
- MAPE: approximately 36%

## Known Limitations

The model is less reliable for rare, high-performance vehicles, due to an insufficient number of such samples in the dataset.

## Future Work

- Polynomial regression (age shows a nonlinear relationship with price)
- Collecting more data for high-power vehicles
- Additional features (equipment, condition, number of previous owners)

## Setup

pip install -r requirements.txt