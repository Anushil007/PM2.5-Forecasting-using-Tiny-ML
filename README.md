# Nepal Air Quality Monitoring and Forecasting Station

## Overview

This repository contains the datasets, data acquisition code, and exploratory data analysis (EDA) for an MSc project focused on developing a local air-quality monitoring and forecasting station for Nepal.

The project uses ground-based air-quality observations from OpenAQ monitoring locations, supplemented by meteorological data from Open-Meteo and atmospheric estimates from the Copernicus Atmosphere Monitoring Service (CAMS).

Hadigaun, Kathmandu, is the primary monitoring location. The project also uses observations from Lalitpur and Pokhara for spatial comparison, and historical PM2.5 observations from Embassy Kathmandu and Phora Durbar for supplementary analysis.

The broader project aims to integrate air-quality monitoring, meteorological information, machine-learning-based forecasting, and deployment on a resource-constrained edge device.

**Current repository scope:** data acquisition, dataset preparation, data quality assessment, and exploratory analysis. Forecasting model development and edge deployment are subsequent project stages.

## Repository Structure

```text
Nepal-Air-Quality-Monitoring/
│
├── dataset/
│   ├── raw_cams_hadigaun.csv
│   ├── raw_data_durbar.csv
│   ├── raw_data_embassy.csv
│   ├── raw_data_hadigaun.csv
│   ├── raw_data_lalitpur.csv
│   ├── raw_data_pokhara.csv
│   ├── raw_master_hadigaun_merged.csv
│   └── raw_weather_data_hadigaun.csv
│
├── curated/
│   ├── cams_curated.csv
│   ├── durbar_curated.csv
│   ├── embassy_curated.csv
│   ├── hadigaun_curated.csv
│   ├── lalitpur_curated.csv
│   ├── master_hadigaun_curated.csv
│   └── pokhara_curated.csv
│
├── notebooks/
│   ├── Data_Acquisition.ipynb
│   └── EDA.ipynb
│
├── data_dictionary.xlsx
├── requirements.txt
└── README.md
```

## Data Sources

### 1. Ground-Based Air Quality Data

Air-quality observations were obtained from [OpenAQ](https://openaq.org/), which aggregates measurements provided by monitoring operators.

| Monitoring location | OpenAQ Location ID | Role |
|---|---:|---|
| Hadigaun, Kathmandu | 2848864 | Primary monitoring location |
| Lalitpur | 6128821 | Contemporary spatial comparison |
| Pokhara | 6118806 | Contemporary spatial comparison |
| Embassy Kathmandu | 3459 | Historical comparison |
| Phora Durbar | 3460 | Historical comparison |

The contemporary Hadigaun, Lalitpur, and Pokhara datasets contain the following variables:

- PM2.5
- PM1
- Temperature
- Relative humidity
- Particle count (0.3 µm channel)

The historical Embassy Kathmandu and Phora Durbar datasets provide PM2.5 observations.

### 2. Meteorological Data

Meteorological data were obtained from the [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api), using the Hadigaun monitoring location coordinates.

The selected weather model was ECMWF IFS, with nearest-grid-cell selection.

The dataset contains 20 hourly meteorological variables, including:

- Temperature, relative humidity, and dew point
- Precipitation and rain
- Wind speed, direction, and gusts
- Surface pressure and mean sea-level pressure
- Total, low, mid, and high cloud cover
- Boundary layer height
- Shortwave, direct, diffuse, and terrestrial radiation
- Sunshine duration

The weather data are model-derived estimates rather than measurements from an instrument located at the monitoring station.

The original weather dataset is retained in `dataset/raw_weather_data_hadigaun.csv` and is used directly in the analysis. Its observations are also incorporated into the Hadigaun master dataset.

### 3. CAMS Atmospheric Data

Supplementary atmospheric data were obtained through the [Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api), using the CAMS global domain.

The dataset contains:

- PM2.5
- PM10
- Nitrogen dioxide (NO₂)
- Sulphur dioxide (SO₂)
- Carbon monoxide (CO)
- Aerosol optical depth at 550 nm

CAMS provides model-derived atmospheric estimates and has a substantially coarser spatial representation than the local monitoring stations. Aerosol optical depth is a column-integrated measure and is not directly equivalent to surface PM2.5 concentration.

CAMS is therefore used for supplementary comparison and atmospheric context, not as a replacement for ground-based observations.

## Dataset Organisation

The repository separates source data, processed datasets, and analysis notebooks.

### `dataset/`

Contains the acquired datasets and the intermediate merged Hadigaun dataset.

The original OpenAQ, weather, and CAMS source files are retained separately. The file `raw_master_hadigaun_merged.csv` is an intermediate dataset combining Hadigaun sensor observations with meteorological data; it is not an untouched source download.

### `curated/`

Contains the processed datasets prepared for analysis.

| Dataset | Rows | Columns | Description |
|---|---:|---:|---|
| Hadigaun | 10,981 | 6 | Primary station observations |
| Hadigaun master | 10,981 | 26 | Hadigaun observations integrated with meteorological variables |
| Lalitpur | 6,000 | 6 | Contemporary spatial comparison |
| Pokhara | 7,783 | 6 | Contemporary spatial comparison |
| Embassy Kathmandu | 19,305 | 2 | Historical PM2.5 observations |
| Phora Durbar | 17,797 | 2 | Historical PM2.5 observations |
| CAMS | 37,200 | 7 | Supplementary atmospheric estimates |

The weather dataset does not have a separate curated CSV. The original weather file is used directly, while the meteorological variables are also included in the curated Hadigaun master dataset.

### `data_dictionary.xlsx`

Provides the dataset inventory and variable-level reference information, including descriptions, units, data types, sources, and relevant processing notes.

## Data Preparation

The preparation workflow applies source-specific cleaning and standardisation while retaining the original source datasets.

Key processing decisions include:

- OpenAQ long-format observations are converted into wide-format datasets.
- Column names are standardised across the curated datasets.
- Timestamps retain their original time-zone conventions and are not arbitrarily shifted or rounded.
- Nepal Time (NPT, UTC+05:45) is used for local station observations; UTC timestamps are retained for weather and CAMS data.
- UTC timestamps are used as the alignment key when integrating Hadigaun observations with meteorological data.
- Invalid negative PM2.5 observations in the historical Embassy and Phora Durbar datasets are treated as missing values.
- Zero readings in the Lalitpur and Pokhara datasets are retained.
- The 72 leading CAMS records with missing values across all six atmospheric variables are excluded from the curated CAMS dataset.
- Missing observations are not artificially filled through imputation or interpolation.
- Boundary layer height gaps are retained as missing values.
- The Hadigaun master dataset is formed by joining meteorological observations onto the Hadigaun station timestamps. Weather-only timestamps do not create additional station records.

Further details about transformations and variable definitions are provided in `data_dictionary.xlsx` and the EDA notebook.

## Notebooks

### 1. `Data_Acquisition.ipynb`

Contains the data acquisition workflow for retrieving the required air-quality, meteorological, and atmospheric datasets.

### 2. `EDA.ipynb`

Contains the exploratory data analysis and dataset assessment, including:

- Data quality and completeness assessment
- Descriptive statistics
- Spatial comparisons between monitoring locations
- Temporal and seasonal pollution patterns
- Daily and weekly variation
- Relationships between air quality and meteorological variables
- Lag, persistence, and CAMS comparisons
- High-pollution episode identification and analysis

## Environment Setup

Python dependencies are listed in `requirements.txt`.

To set up the environment:

```bash
git clone <repository-url>
cd Nepal-Air-Quality-Monitoring

pip install -r requirements.txt
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open the notebooks from the `notebooks/` directory.

## Important Notes

- Ground-based observations, meteorological estimates, and CAMS estimates have different sources, measurement characteristics, and spatial representations. They should not be treated as interchangeable.
- Particle-count measurements are retained as reported by the source; their magnitude and precise size interpretation should be considered alongside the source metadata.
- Missing values are preserved where observations are unavailable rather than replaced with fabricated measurements.
- Exploratory relationships and correlations do not establish causation.
- The current analysis does not constitute a validated forecasting model or a completed edge-deployment system.
