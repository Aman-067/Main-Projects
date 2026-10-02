# Data Accessing and Cleaning (Pandas)

Notebook: `DA.ipynb`

## Goal
Take the raw Stack Overflow 2025 survey (49,191 responses, 172 columns) and turn it into a smaller, readable dataset focused on who developers are and how they use AI.

## Tools
Python · Pandas · Jupyter Notebook

## Layers in the notebook

**Layer 1: Initial data inspection**
- Load the dataset and look through it manually to see what kind of values it holds

**Layer 2: Data profiling**
- Pandas operations to understand the columns: shape, dtypes, null counts, unique values

**Layer 3: Data wrangling, exploratory visualization and anomaly detection**
- Select the final columns: kept 32 (profile, work, tech stack, AI usage and opinions)
- Standardise values: shortened long survey labels with `replace` dictionaries
- Group categories: `DevType` grouped into broader job families
- Simplify answers:
  - `LearnCodeAI` reduced to Yes / No
  - `AILearnHow` keeps only the first listed option
  - `AIFrustration` kept as `;` separated combinations
- Rename columns to readable names (e.g. `ConvertedCompYearly` → `Salary_USD`)
- Drop `LearnCode` (not relevant to the AI theme)
- Handle outliers: created `Salary_clean`, `Work_exp_clean`, `Years_coding_clean`; raw columns kept
- Optimise dtypes: `float32` for salary, `Int8` for ratings and experience
- Export the cleaned CSV (UTF-8, no index)

## Key decisions
- Nulls left as NaN where the question was not asked; no global `dropna()`
- "Prefer not to say" answers labelled `Not mentioned`
- Salary outliers (e.g. 1.0 USD, 50,000,000 USD) set to NaN in the clean column only, rows kept
- Experience capped at 65 years in the clean columns

## Result
- 172 → 34 columns (32 selected + 3 `_clean` columns − 1 dropped), 49,191 rows kept
- File size: ~134 MB → ~20 MB

## Output
Cleaned file: `../Data/stackoverflow_survey_clean.csv`
