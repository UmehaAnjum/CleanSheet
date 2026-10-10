# CleanSheet
A Python-based CSV Data Quality Auditor that detects missing values, duplicate rows, invalid ages, and invalid emails, and generates quality reports.
# CleanSheet — CSV Data Quality Auditor

CleanSheet is a Python-based project that audits CSV datasets and generates reports to help identify common data quality problems.

## Features

- **Dataset overview:** Displays the number of rows and columns.
- **Missing-value analysis:** Counts missing values and calculates their percentages for each column.
- **Duplicate detection:** Identifies duplicate rows.
- **Empty-row and empty-column detection:** Finds rows or columns containing only missing values.
- **Data type inspection:** Reports the data type of each column.
- **Validation checks:** Detects invalid ages using a 0–120 range and checks email formats when an `Email` column is present.
- **Quality warnings:** Assigns HIGH, MEDIUM, or LOW severity based on the percentage of affected rows.
- **CSV report export:** Saves the quality warnings as a CSV file.

## Technologies Used

- Python
- Pandas
- Google Colab
- GitHub

## Dataset and Testing

The project was tested using the Titanic training dataset and a small synthetic dataset designed to contain data quality issues.

The Titanic dataset contains 891 rows and 12 columns. The audit identified missing values in `Age` (177), `Cabin` (687), and `Embarked` (2).

The synthetic dataset was used to test duplicate detection, missing values, invalid ages, and invalid email formats.

## How to Run

1. Open `CleanSheet_CSV_Data_Quality_Auditor.ipynb`.
2. Open the notebook in Google Colab.
3. Upload the CSV file you want to audit, or update the file path in the notebook.
4. Run the notebook cells in order.
5. Review the audit results and export the generated quality report.

## Limitations

- The current checks focus on common data quality issues.
- Age and email validation are applied only when the corresponding columns are present.
- Severity levels are based on predefined percentage thresholds.
- The project identifies issues; it does not automatically repair the dataset.

## Future Improvements

- Support CSV uploads through a simple user interface.
- Add configurable validation rules.
- Generate downloadable reports with charts.
- Add more data-quality checks and automated tests.

## Author

**Umeha Anjum**

