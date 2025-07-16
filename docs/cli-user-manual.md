# User Manual

The `ffaframework.R` script runs the complete workflow for Exploratory Data Analysis (EDA) and Flood Frequency Analysis (FFA).

## Configuration Reference

All settings are controlled via the `config.yml` file, written in [YAML](https://learnxinyminutes.com/yaml/).

### Data Preparation

**`data_source`** (required): Character (1); Source of input data. Options:
- `"Local"`: Use local **`csv_files`** files containing the data.
- `"GeoMet"`: Download data from the [MSC GeoMet API](https://www.canada.ca/en/environment-climate-change/services/weather-general-tools-resources/weather-tools-specialized-data/msc-geomet-api-geospatial-web-services.html) using **`station_ids`**.

**`csv_files`**: Character; CSV files located in the `/data` directory.

**`station_ids`**: Character; Hydrometric station IDs. Search by name, province, basin, or location [here](https://wateroffice.ec.gc.ca/search/real_time_e.html). Some stations may have little or no data.

### Exploratory Data Analysis (EDA)

**`split_selection`**: Character (1); Method to determine change points and split dataset into homogeneous sub-periods (if applicable):

- `"Automatic"`: Detect and split automatically.
- `"Manual"`: Detect and ask for user confirmation.
- `"Preset"`: Use predefined values from **`split_points`** (see below).

**`split_points`**: Integer; predefined change points; use `null` for none. 

**`significance_level`**: Numeric (1); significance level (between `0.01` and `0.1`).

**`bbmk_samples`**: Integer (1); number of bootstrap samples for the [BB-MK Test](eda-trend-ams-mean.md/#bb-mk-test).

### Distribution Selection

**`distribution_selection`**: Character (1); Metric for [distribution selection](model-selection.md):

- `"L-distance"`: Euclidean distance from (L-skewness, L-kurtosis) point.
- `"L-kurtosis"`: Difference between theoretical and sample L-kurtosis. 
- `"L-statistic"`: Bootstrapped Z-statistic computed using the Kappa distribution.
- `"Preset"`: Pre-defined distribution with the **`distribution_name`** option.

**`distribution_name`**: Character (1); used only if `distribution_selection = "Preset"`. Must match a supported [distribution name](probability-distributions.md).

**`z_samples`**: Integer (1); number of bootstrap samples for [Z-statistic selection](model-selection.md#z-statistic).

### Parameter Estimation

**`s_estimation`** / **`SFFA_model_fit`**: Character (1); Method for [estimating parameters](parameter-estimation.md) in stationary models:

- `"L-moments"`: Method of L-moments using formulas from Hosking (1997).
- `"MLE"`: Maximum likelihood estimation.
- `"GMLE"`: Generalized maximum likelihood estimation (for GEV distribution only).

**`ns_estimation`** / **`NSFFA_model_fit`**: Character (1); Method for estimating parameters in nonstationary models:

- `"MLE"`: Maximum likelihood estimation.
- `"GMLE"`: Generalized maximum likelihood estimation (for GEV distribution only).

**`gev_prior`**: Numeric (2); geophysical prior's (beta distribution) parameters `(p, q)` for the GEV shape parameter. If using `"MLE"` or `"RFPL"` (see below), set this option to `null`. 

### Uncertainty Quantification

**`s_uncertainty`**  / **`SFFA_uncertainty`**: Character (1); [uncertainty quantification](uncertainty-quantification.md) method for stationary models:

- `"Bootstrap"`: Parametric bootstrap.
- `"RFPL"`: Regula-falsi profile likelihood (MLE only).
- `"RFGPL"`: Generalized regula-falsi profile likelihood (GMLE only).

**`ns_uncertainty`**  / **`NSFFA_uncertainty`**: Character (1); uncertainty quantification method for nonstationary models:

- `"Bootstrap"`: Parametric bootstrap.
- `"RFPL"`: Regula-falsi profile likelihood (MLE only).
- `"RFGPL"`: Generalized regula-falsi profile likelihood (GMLE only).

**`return_periods`**: Numeric; list of return periods (in years) to estimate return levels.

**`sb_samples`**  / **`bootstrap_samples`**: Integer (1); number of samples for [bootstrap uncertainty quantification](uncertainty-quantification.md#sample-bootstrap).

**`rfpl_tolerance`**: Numeric (1); log-likelihood tolerance for [RFPL uncertainty quantification](uncertainty-quantification.md#regula-falsi-profile-likelihood-rfpl).

### Model Assessment

**`pp_formula`**: Character (1); plotting position formula for [model assessment](model-assessment.md). Must be one of: 

- `"Weibull"`: $i / (n + 1)$
- `"Blom"`: $(i - 0.375) / (n + 0.25)$
- `"Cunnane"`: $(i - 0.4) / (n + 0.2)$
- `"Gringorten"`: $(i - 0.44) / (n + 0.12)$
- `"Hazen"`: $(i - 0.5) / n$

### Plot Generation

**`show_trend`**: Boolean (1); if `true`, a trend line is added to the AMS data (where applicable). 

**`slices`**: Integer; Specific years to estimate return levels for nonstationary models. Out-of-range years are ignored.

### Report Generation

**`generate_report`**: Boolean (1); if `true`, generates a report in `.html` format.
