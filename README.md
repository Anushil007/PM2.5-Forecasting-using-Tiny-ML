# Nepal Air Quality Monitoring Station – MSc Project

## Project Overview

This repository contains the datasets and Python notebooks developed for the MSc project on a Nepal Air Quality Monitoring Station.

The project focuses on air-quality data acquisition, curation, exploratory data analysis, and the development of a system for monitoring air quality and predicting near-future pollution levels.

## Repository Structure

```text
repository/
│
├── dataset/
│   ├── master_hadigaun_merged_raw.csv
│   ├── raw_data_durbar.csv
│   ├── raw_data_embassy.csv
│   ├── raw_data_hadigaun.csv
│   ├── raw_data_lalitpur.csv
│   ├── raw_data_pokhara.csv
│   └── weather_data_hadigaun.csv
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
├── requirements.txt
├── data_dictionary.xlsx
└── README.md
```

## Dataset Description

### 1. Raw Datasets — `dataset/`

Contains the acquired datasets before the final curation process.

| File | Description |
|---|---|
| `raw_data_hadigaun.csv` | Raw air-quality observations from Hadigaun |
| `raw_data_lalitpur.csv` | Raw air-quality observations from Lalitpur |
| `raw_data_pokhara.csv` | Raw air-quality observations from Pokhara |
| `raw_data_embassy.csv` | Raw air-quality observations from the Embassy station |
| `raw_data_durbar.csv` | Raw air-quality observations from the Durbar station |
| `master_hadigaun_merged_raw.csv` | Merged raw dataset associated with the Hadigaun monitoring location |
| `weather_data_hadigaun.csv` | Meteorological data associated with Hadigaun |

### 2. Curated Datasets — `curated/`

Contains the processed datasets prepared for exploratory analysis and subsequent modelling.

| File | Description |
|---|---|
| `hadigaun_curated.csv` | Curated Hadigaun air-quality dataset |
| `lalitpur_curated.csv` | Curated Lalitpur air-quality dataset |
| `pokhara_curated.csv` | Curated Pokhara air-quality dataset |
| `embassy_curated.csv` | Curated Embassy air-quality dataset |
| `durbar_curated.csv` | Curated Durbar air-quality dataset |
| `master_hadigaun_curated.csv` | Integrated Hadigaun dataset with air-quality and meteorological variables |
| `cams_curated.csv` | Curated CAMS dataset used for comparison with ground-level observations |

## Notebooks

The `notebooks/` directory contains the Python notebooks used in the project.

- **`Data_Acquisition.ipynb`** — Data acquisition and extraction workflows.
- **`EDA.ipynb`** — Data auditing, curation-related analysis, statistical summaries, and exploratory data analysis.

## Data Dictionary

`data_dictionary.xlsx` documents the datasets, including variable names, descriptions, units, data types, and other relevant information.

## Environment Setup

Install the required Python packages using:

```bash
pip install -r requirements.txt
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open the relevant notebook from the `notebooks/` directory.

## Notes

- Raw and curated datasets are maintained separately.
- The curated datasets are intended for analysis and subsequent modelling.
- The notebooks provide the computational workflows used in the project.
- Project reports and detailed research documentation are maintained separately from this repository.
