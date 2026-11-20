# Nepal Air Quality Monitoring – MSc Project

## Stage 4: Data Acquisition, Curation and Exploratory Data Analysis

This repository contains the datasets, Jupyter notebooks, and supporting files developed during Stage 4 of the MSc project. The work focuses on acquiring air-quality and meteorological data, preparing curated datasets, and conducting exploratory data analysis to characterize particulate matter concentrations and their temporal, spatial, and meteorological relationships.

## Repository Structure

```text
nepal-air-quality-station-msc/
│
├── datasets/
│   ├── raw/
│   │   ├── OpenAQ/
│   │   ├── OpenMeteo/
│   │   └── CAMS/
│   │
│   └── curated/
│       ├── hadigaun_curated.csv
│       ├── master_hadigaun_curated.csv
│       ├── lalitpur_curated.csv
│       ├── pokhara_curated.csv
│       ├── embassy_curated.csv
│       ├── durbar_curated.csv
│       └── cams_curated.csv
│
├── notebooks/
│   ├── 01_data_extraction.ipynb
│   └── 02_eda.ipynb
│
├── requirements.txt
├── data_dictionary.xlsx
└── README.md
```

## Dataset Description

### 1. Raw Datasets

The `datasets/raw/` directory contains the original acquired datasets, organized by their respective sources:

- **OpenAQ:** Ground-based air-quality observations from monitoring locations.
- **Open-Meteo:** Meteorological observations and reanalysis data.
- **CAMS:** Copernicus Atmosphere Monitoring Service data used for comparison with ground-based PM2.5 observations.

Raw data are retained separately from the curated datasets to preserve the original source records.

### 2. Curated Datasets

The `datasets/curated/` directory contains the processed datasets prepared for Stage 4 analysis.

| Dataset | Description |
|---|---|
| `hadigaun_curated.csv` | Primary Hadigaun air-quality and sensor observations |
| `master_hadigaun_curated.csv` | Matched Hadigaun air-quality and meteorological dataset |
| `lalitpur_curated.csv` | Curated air-quality observations from Lalitpur |
| `pokhara_curated.csv` | Curated air-quality observations from Pokhara |
| `embassy_curated.csv` | Historical air-quality observations from the Embassy monitoring location |
| `durbar_curated.csv` | Historical air-quality observations from the Durbar monitoring location |
| `cams_curated.csv` | Curated CAMS data used for comparison with ground-based observations |

The datasets support temporal, spatial, meteorological, and pollution-episode analyses.

## Notebooks

The `notebooks/` directory contains the executable Jupyter notebooks used for data acquisition and exploratory analysis.

- **`01_data_extraction.ipynb`** – Data acquisition and extraction procedures for the datasets used in the project.
- **`02_eda.ipynb`** – Data auditing, curation, statistical summaries, spatial and temporal analysis, meteorological analysis, lag analysis, and high-pollution episode analysis.

The notebooks document the analytical workflow and support reproducibility of the Stage 4 results.

## Data Dictionary

`data_dictionary.xlsx` provides descriptions of the datasets and their variables, including variable names, definitions, measurement units, data sources, and relevant processing information.

## Environment Setup

The project uses Python and Jupyter Notebook.

To install the required Python dependencies, create and activate a virtual environment, then execute:

```bash
pip install -r requirements.txt
```

To launch Jupyter Notebook:

```bash
jupyter notebook
```

## Notes

- Raw and curated datasets are maintained separately.
- Timestamps and measurement units should be interpreted according to the relevant dataset documentation and data dictionary.
- The accompanying project report documents the data preparation decisions, transformations, analytical methods, results, and limitations.
- This repository currently covers **Stage 4 only**. Subsequent project stages will be incorporated as development progresses.
