# Data

Cleaned dataset for the Stack Overflow AI Survey project.

## Source
Original survey: Stack Overflow Developer Survey 2025 (https://survey.stackoverflow.co), licensed under ODbL.
Copy of the dataset used: [stackoverflow_survey_2025.csv](https://github.com/akshara-a/open-data-intelligence-hub/blob/main/Stack%20Overflow%20Survey%20-%202025/dataset/stackoverflow_survey_2025.csv) from the open-data-intelligence-hub repo by akshara-a.
The original file is not included here.

## Files
- `stackoverflow_survey_clean.csv`: cleaned dataset (49,191 rows, 34 columns, ~20 MB)

## Tools
Python · Pandas · Jupyter Notebook 

## Layer-wise process

**Layer 1: Raw data**
- Original survey: 49,191 responses, 172 columns (~134 MB)

**Layer 2: Column selection (Pandas)**
- Kept 32 columns about who the developer is and how they use AI
- Dropped the rest (tech endorsements, job-satisfaction points, OS, tools, Stack Overflow habits, etc.)

**Layer 3: Value standardisation (Pandas)**
- Shortened long survey labels (e.g. `Bachelor’s degree (B.A., B.S., B.Eng., etc.)` → `Bachelor`)
- Grouped `DevType` into broader job families (renamed `Job_title`)
- Renamed AI answers to a consistent style (`Yes - daily`, `No - but want to`, ...)
- Renamed columns to readable names (e.g. `ConvertedCompYearly` → `Salary_USD`)
- Multi-select columns (`;` separated) kept as they are; `AI_learning_source` keeps the first listed option only

**Layer 4: Outlier handling (Pandas)**
- Raw numeric columns kept untouched
- Added `Salary_clean` (kept between 800 and 500,000 USD), `Work_exp_clean` and `Years_coding_clean` (kept up to 65 years); values outside the limits are NaN
- Rows were not deleted, so AI answers from those respondents stay in the data

**Layer 5: Memory optimisation**
- Salary columns → `float32`, ratings and experience → `Int8`
- Together with dropping unused columns: ~134 MB → ~20 MB

**Layer 6: Export**
- Saved as CSV (UTF-8, without the index) for SQL

## Next layers
- SQL EDA in MySQL
- Power BI dashboard

## Notes
- Empty cells mean the question was not asked or not answered
- `Not mentioned` means the respondent chose "prefer not to say"
