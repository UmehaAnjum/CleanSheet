# CleanSheet — CSV Data Quality Auditor & Cleaner

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/UmehaAnjum/CleanSheet/blob/main/notebooks/cleansheet_data_quality_auditor_and_cleaner.ipynb)

CleanSheet is a Python/pandas notebook that detects common data-quality issues in CSV datasets and cleans them using configurable rules. It generates a quality report, applies the selected cleaning operations to a **copy** of the data, and exports the cleaned dataset together with a cleaning log.

It was built with Python, pandas, and Google Colab as a learning and demonstration project.

## Repository Structure

```
CleanSheet/
├── notebooks/
│   └── cleansheet_data_quality_auditor_and_cleaner.ipynb   # The CleanSheet notebook
├── data/
│   └── train.csv                  # Input: Titanic training dataset (891 rows, 12 columns)
├── outputs/                       # Results of the tested run on train.csv
│   ├── cleansheet_cleaned.csv
│   ├── cleansheet_quality_report.csv
│   └── cleansheet_cleaning_log.csv
├── requirements.txt
├── .gitignore
└── README.md
```

## Features

### 1. Data quality auditing

CleanSheet checks a dataset for:

- Missing values
- Duplicate rows
- Empty rows and columns
- Data types
- Invalid age values
- Invalid email formats

The quality report contains the column name, issue detected, number of affected records, percentage of affected records, and severity (`HIGH` ≥ 50%, `MEDIUM` ≥ 10%, otherwise `LOW`).

### 2. Data cleaning

| Option | Default | Behaviour |
|---|---|---|
| Remove duplicate rows | on | Drops exact duplicate rows |
| Validate ages | on | Ages below 0 or above 120 become missing values |
| Validate email formats | on | Invalid email formats become missing values |
| Fill missing numeric values | on | Fills with the column median |
| Fill missing text values | off | Fills with the column mode |

Cleaning always runs on a separate copy, so the original DataFrame is left unchanged.

### 3. Interactive controls

In Google Colab the options above appear as `ipywidgets` checkboxes. Click **Clean My Dataset** to run, then **Download All CleanSheet Outputs** to download a ZIP of the results.

### 4. Output files

| File | Purpose |
|---|---|
| `cleansheet_cleaned.csv` | Dataset after the selected cleaning operations |
| `cleansheet_quality_report.csv` | Issues detected in the original dataset, before cleaning |
| `cleansheet_cleaning_log.csv` | Cleaning actions and the number of records affected |
| `cleansheet_outputs.zip` | Created by the download button; contains the three files above |

## How It Works

1. Load a CSV dataset into the notebook.
2. Inspect the dataset and identify data-quality issues.
3. Generate a quality report for the original dataset.
4. Select the desired cleaning operations.
5. Apply the selected rules to a copy of the dataset.
6. Generate a cleaning log.
7. Export the cleaned dataset and reports.
8. Download all outputs as a ZIP file.

## Getting Started

### Option A — Google Colab (recommended)

The notebook was written for Colab and uses Colab's `/content/` working directory and `google.colab.files` for downloads.

1. Click the **Open In Colab** badge above (or upload the notebook from `notebooks/` to Colab).
2. Upload `data/train.csv` (or your own CSV) to the Colab runtime so it is available at `/content/train.csv`. To use a different file, edit the `pd.read_csv(...)` path in the first cell.
3. Run the cells in order.
4. Review the quality report and choose your cleaning options.
5. Click **Clean My Dataset**, then **Download All CleanSheet Outputs**.

### Option B — Local Jupyter

```bash
git clone https://github.com/UmehaAnjum/CleanSheet.git
cd CleanSheet
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

The notebook still contains Colab-specific code: the `/content/...` file paths and the `google.colab.files` download cells. When running locally, change the paths (for example to `../data/train.csv` and `../outputs/`) and skip the download cells.

> **Note:** The notebook redefines `generate_quality_warnings` in a later cell with added age and email checks. Run the cells in order so the final definition is the one used.

## Dataset Testing

CleanSheet was tested on the Titanic training dataset and on a small synthetic dataset with known issues.

### Titanic results (`data/train.csv` → `outputs/`)

The dataset has 891 rows and 12 columns. The quality report found:

| Column | Issue | Count | Percentage | Severity |
|---|---|---:|---:|---|
| Age | Missing values | 177 | 19.87% | MEDIUM |
| Cabin | Missing values | 687 | 77.10% | HIGH |
| Embarked | Missing values | 2 | 0.22% | LOW |

In the tested cleaning run:

- The cleaned dataset kept all 891 rows; no duplicates were found.
- The 177 missing `Age` values were filled with the median.
- Missing `Cabin` and `Embarked` values remained because categorical filling was disabled.

### Synthetic dataset

A small dataset with duplicate rows, a missing age, invalid ages, a missing email, and a malformed email verified that:

- Duplicate rows can be removed.
- Invalid ages are handled.
- Invalid email formats are replaced with missing values.
- Missing numeric values are filled with the median.
- Cleaning options can be customised.
- The original DataFrame remains unchanged.

## Limitations

- Cleaning uses predefined rules and may not suit every dataset.
- Median filling is not appropriate for every numeric column, and mode filling is not appropriate for every categorical column.
- Email validation only checks basic format; it does not verify that an address exists.
- Age cleaning applies to columns named `Age` (case-insensitive); email cleaning applies to columns whose names contain `email`. The audit and quality report check only columns named exactly `Age` and `Email`.
- Invalid values become missing values before the selected filling operation is applied.
- The quality report describes the original dataset only; a separate post-cleaning audit would be needed to summarise remaining issues.
- Review the cleaned output before using it for important decisions.

## Future Improvements

- Add a post-cleaning quality audit.
- Support custom validation rules for different columns.
- Provide before-and-after quality summaries.
- Improve row-level cleaning logs.
- Add support for more input and output formats.
- Develop a more user-friendly interface.

## Author

**Umeha Anjum**
