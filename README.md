# CleanSheet
A Python-based CSV Data Quality Auditor that detects missing values, duplicate rows, invalid ages, and invalid emails, and generates quality reports.
# CleanSheet — CSV Data Quality Auditor & Cleaner

## Overview

CleanSheet is a Python-based tool that detects common data quality issues in CSV datasets and helps users clean their data using configurable cleaning rules.

The project was developed using Python, Pandas, and Google Colab. It aims to make data quality checking and basic data cleaning easier, more organized, and accessible to users.

CleanSheet generates a quality report, applies selected cleaning operations to a copy of the original dataset, and exports the cleaned data and cleaning log as downloadable files.

## Features

### 1. Data Quality Auditing

CleanSheet checks CSV datasets for common data quality problems, including:

- Missing values
- Duplicate rows
- Empty rows and columns
- Data types
- Invalid age values
- Invalid email formats

It generates a structured quality report containing:

- Column name
- Issue detected
- Number of affected records
- Percentage of affected records
- Severity level

### 2. Data Cleaning

CleanSheet supports configurable cleaning operations:

- **Duplicate removal:** Removes duplicate rows when enabled.
- **Missing numeric values:** Fills missing numeric values using the column median when enabled.
- **Missing categorical values:** Optionally fills missing categorical values using the column mode.
- **Age validation:** Treats ages below 0 or above 120 as invalid.
- **Email validation:** Detects basic email-format errors in applicable columns.
- **Original data preservation:** Performs cleaning on a separate copy of the input DataFrame.

### 3. Interactive Cleaning Options

Users can select cleaning operations through interactive checkboxes in Google Colab.

Available options:

- Remove duplicate rows
- Fill missing numeric values with the median
- Fill missing text values with the mode
- Validate ages (0–120)
- Validate email formats

This allows users to customize the cleaning process according to their needs.

### 4. Export and Download

CleanSheet generates the following output files:

| File | Purpose |
|---|---|
| `cleansheet_cleaned.csv` | Contains the dataset after selected cleaning operations |
| `cleansheet_quality_report.csv` | Reports data quality issues detected before cleaning |
| `cleansheet_cleaning_log.csv` | Records cleaning actions and affected counts |
| `cleansheet_outputs.zip` | Contains all three output files |

## How It Works

The workflow follows these steps:

1. Load a CSV dataset into the notebook.
2. Inspect the dataset and identify data quality issues.
3. Generate a quality report describing the original dataset.
4. Select the desired cleaning operations.
5. Apply the selected rules to a copy of the dataset.
6. Generate a cleaning log.
7. Export the cleaned dataset and reports.
8. Download all outputs in a ZIP file.

## Technologies Used

- **Python** — Core programming language
- **Pandas** — Data manipulation, validation, and cleaning
- **Google Colab** — Development and execution environment
- **IPyWidgets** — Interactive cleaning controls
- **CSV and ZIP utilities** — Output generation and download

## Dataset Testing

The project was tested using the Titanic training dataset and a synthetic dataset containing known data quality issues.

### Titanic Dataset Results

The Titanic training dataset contained 891 rows and 12 columns.

The original quality report identified the following missing values:

| Column | Issue | Count | Percentage | Severity |
|---|---|---:|---:|---|
| Age | Missing values | 177 | 19.87% | MEDIUM |
| Cabin | Missing values | 687 | 77.10% | HIGH |
| Embarked | Missing values | 2 | 0.22% | LOW |

During the tested cleaning run:

- The original dataset contained 891 rows.
- The cleaned dataset contained 891 rows.
- No duplicate rows were removed.
- The 177 missing Age values were filled using the median.
- Missing Cabin and Embarked values remained because categorical filling was disabled.

### Synthetic Dataset Testing

A small test dataset was created with duplicate rows, missing ages, invalid ages, missing emails, and an invalid email format.

The tests verified that:

- Duplicate rows could be removed.
- Invalid ages could be handled.
- Invalid email formats could be replaced with missing values.
- Missing numeric values could be filled using the median.
- Users could customize cleaning options.
- The original DataFrame remained unchanged.

## How to Run the Project

1. Open the project notebook in Google Colab.
2. Upload the notebook if it is not already available in your Drive.
3. Upload your CSV dataset or update the dataset-loading code to point to your file.
4. Run the notebook cells in order.
5. Review the generated quality report.
6. Select your preferred cleaning options.
7. Click **Clean My Dataset**.
8. Click **Download All CleanSheet Outputs** to download the generated files.

**Important:** If the notebook loads `/content/train.csv`, that file must be uploaded to the Colab runtime first, or the loading code must be updated to use your own CSV file. The interactive workflow uses the DataFrame stored in `df`.

## Limitations

- Cleaning operations use predefined rules and may not suit every dataset.
- Median filling is not appropriate for every numeric column.
- Mode filling may not be appropriate for every categorical column.
- Basic email-format validation does not verify whether an email address exists.
- Age validation applies to columns named `Age`, regardless of capitalization.
- Email validation applies to columns whose names contain `email`.
- Invalid values may become missing values before the selected filling operation is applied.
- The quality report describes issues found in the original dataset; a separate post-cleaning audit would be needed to summarize all remaining issues.
- Users should review the cleaned output before using it for important decisions.

## Future Improvements

- Add a post-cleaning quality audit.
- Support custom validation rules for different columns.
- Provide before-and-after quality summaries.
- Improve row-level cleaning logs.
- Add support for more input and output formats.
- Develop a more user-friendly interface.

## Author

**Umeha Anjum**



CleanSheet is a learning and demonstration project focused on data quality auditing and configurable CSV cleaning. The project preserves the original input DataFrame and creates separate output files for the cleaned data and reports.
