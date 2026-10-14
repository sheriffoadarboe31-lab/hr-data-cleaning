================================================================
DATA CLEANING WORKFLOW: HR DATASET
================================================================

PROJECT OVERVIEW
----------------
This project contains a complete data cleaning and preprocessing
pipeline applied to the raw HR dataset (Prac_Sql.csv). The goal
was to ensure data integrity, remove inconsistencies, fix data
types, and handle missing values so the dataset is ready for
analysis or SQL practice.

The cleaning process was performed in Python using the Pandas
library inside a Jupyter Notebook.

================================================================
CLEANING ORDER & STEPS COMPLETED
================================================================

The data was processed in the following sequence to ensure
dependencies were handled correctly (e.g., fixing data types
before handling missing values).

1. COLUMN REDUCTION (DROPPING EMPTY COLUMNS)
   Removed extraneous columns that contained no useful data,
   such as automatically generated columns like "Unnamed: 9".

2. TEXT TRIMMED (NAME)
   Cleaned the "Name" column by stripping leading and trailing
   whitespace and using regex to replace multiple internal
   spaces with a single space.

3. EXACT AND SAME-ID DUPLICATES HANDLED
   - Removed exact full-row duplicates to prevent double-counting.
   - Dropped compound duplicates based on Emp_ID and Department,
     keeping only the first occurrence per employee per department.

4. TYPES FIXED (SALARY, DATES)
   - Salary: Stripped currency symbols ($), whitespace, and
     commas, then converted the column to a numeric format.
     Used errors="coerce" to safely turn invalid entries into NaN.
   - Dates: Converted the start date column to a standard
     datetime format (%d/%m/%y).

5. MISSING VALUES HANDLED (NUMERICAL & CRITICAL)
   - Dropped rows where the critical identifier Emp_ID was missing.
   - Replaced 0 values in the Salary column with NaN (since a $0
     salary is likely a data entry error) and dropped any
     resulting nulls.

6. MISSING VALUES HANDLED (CATEGORICAL IMPUTATION)
   Filled missing values in the "Gender" and "Department" columns
   with the placeholder string "Unknown" to preserve the rows
   without introducing bias.

7. FINAL VALIDATION & DATA PROFILING
   - Date Sanity Check: Verified the min and max dates to
     ensure all entries fall within a reasonable range
     (2018-01-29 to 2021-11-10).
   - Categorical Distribution: Used value_counts(dropna=False)
     on key categorical columns (Gender, Department,
     Employee_type, Work_location) to verify data consistency
     and confirm no unexpected nulls remained.

================================================================
FINAL OUTPUT
================================================================

The final cleaned dataset was saved as:

    hr_clean_in_pytn.csv

Note: The index was set to False during export so that Pandas
does not write a redundant row number column into the CSV file.

================================================================
HOW TO USE
================================================================

To load and explore the cleaned dataset in Python:

    import pandas as pd

    # Load the cleaned dataset
    df_clean = pd.read_csv("hr_clean_in_pytn.csv")

    # Display the first few rows
    display(df_clean.head())

================================================================