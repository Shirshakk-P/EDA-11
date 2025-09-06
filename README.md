# Renewable Energy Datasets:

---

### Additional Dataset: 

[kaggle/bda-assignment1](https://www.kaggle.com/datasets/shirshakkp/bda-assignment1)
(tif files for wind_speeds)

Files:  (also the same order for running them)

1. 1_data_extraction.ipynb: Data Fetching python notebook
2. ML-tasks.ipynb: Notebook that uses forecasting to predict capacities (Wind, Solar, Renewable Energy).
3. Formulas.pdf: document containing all the neccessary formulas used to calculate the Wind and Solar Energy outputs.
4. merger.ipynb: Python script to merge the outputs into an integrated csv file.
5. merged_us_city_data: Final integrated Dataset (in csv)

---
final_dataset: folder that contains all the extracted data in csv format.

---

Forecasting Models used:

1. Linear Regression
2. Random Forest with 100 estimators
3. 5-layered Neural Network (ReLU activations, 128>64>32>16>1 neurons) 

---

## 1. Wind Dataset (`atlas.csv`) [US Locations only]

### Overview

This dataset contains wind resource information collected at various heights and geographic locations (cities/states). It is primarily used for wind speed estimation and power capacity calculation analyses.

### Key Columns

- **city**: Name of the city or location where measurements are taken.
- **state**: Name of the state or region for the city.
- **wind_speed_50m**: Measured or simulated wind speed at 50 meters height (m/s).
- **wind_speed_100m**: Measured or simulated wind speed at 100 meters height (m/s).
- **wind_speed_150m**: Measured or simulated wind speed at 150 meters height (m/s).
- **wind_speed_80m_est** (added post forecasting): Estimated wind speed at 80 meters using logarithmic wind profile approximation.
- **power_80m_est** (added post forecasting): Estimated wind power generated at 80 meters height, calculated using \(P = 0.5 \times \rho \times A \times v^3 \times \text{efficiency}\).

### Usage Notes

- <wind_data_at_xyz_m.tif> : raster files for wind speeds at xyz elevation >> Processed using 'rasterio' python library to produce csv files.
- Wind speed values at different heights are used to model vertical wind profiles.
- Power estimates use wind speed cubed relationship and take air density (\(\rho\)), rotor swept area (\(A\)) and turbine efficiency into account.
- Useful for estimating wind energy potential in specific regions.

---

## 2. Solar Dataset (`nrel_solar_data_full_combined.csv`) [US Locations only]

### Overview

This dataset contains solar irradiance data for sites including Global Horizontal Irradiance (GHI), Direct Normal Irradiance (DNI), Diffuse Horizontal Irradiance (DHI), and solar tilt radiation data computed at annual and monthly scale.

### Key Columns

- **annual_dni**: Annual Direct Normal Irradiance values (W/m²), stored as stringified dictionaries with annual and monthly values.
- **annual_tilt**: Annual solar radiation values on a tilted plane (W/m²), also stored as stringified dictionaries.
- **annual_dhi** (added): Estimated annual Diffuse Horizontal Irradiance, computed as observed solar radiation minus component from DNI.
- **annual_ghi_calc** (added): Calculated annual Global Horizontal Irradiance using \( \text{GHI} = \text{DNI} \times \cos(\theta) + \text{DHI} \).
- **monthly_ghi_vals** (added): Monthly GHI values extracted and ordered from the data.
- **solar_power_generated** (added): Solar power generated in watts, calculated using panel area and efficiency times the actual annual GHI.

### Usage Notes

- Monthly and annual GHI data are used for solar resource assessment.
- Calculations incorporate empirical adjustments such as cosine tilt factor.
- Useful for forecasting solar power potential and designing solar energy systems.

---

## 3. IRENA Dataset (`IRENA.csv`)	[Worldwide Locations]

### Overview

This dataset contains country-level renewable energy metrics from the International Renewable Energy Agency (IRENA), reporting shares of renewable electricity capacity and generation percentages annually over multiple years (2000–2024).

### Key Columns

- **Region/country/area**: The country or regional entity for the data row.
- **Year**: The calendar year of the data point.
- **Indicator**: Specifies the metric—either `"RE share of electricity capacity (%)"` or `"RE share of electricity generation (%)"`.
- **Renewable energy share of electricity capacity and generation (%)**: Percentage value of renewable share in capacity or generation.

### Usage Notes

- Forecasting models apply to predict capacity and generation shares for future year(2025).
