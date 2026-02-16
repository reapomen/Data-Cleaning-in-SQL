# Data-Cleaning-in-SQL
This project demonstrates a complete SQL-based data cleaning pipeline applied to a global layoffs dataset.   
The workflow preserves raw data, removes duplicates, standardizes values, and imputes missing fields to prepare the dataset for reliable analysis.

# 🧼 Layoffs Dataset Cleaning — SQL Portfolio Project


## 📁 Dataset
**Source Table:** `layoffs`  
**Staging Tables:**  
- `layoffs_staging` — raw copy for safe manipulation  
- `layoffs_staging2` — cleaned and normalized dataset  

**Key Fields:**  
- company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised_millions

---

## 🔍 Cleaning Steps

### STEP 1: Preserve Original Data
- Created `layoffs_staging` as a copy of the raw dataset to ensure the original data remains intact.

### STEP 2: Inspect Raw Data
- Queried the staging table to understand structure and anomalies.

### STEP 3–4: Identify & Remove Duplicates
- Used `ROW_NUMBER()` with a CTE to flag duplicate rows.
- Deleted duplicates based on `employee_id`.

### STEP 5–7: Create Secondary Staging Table
- Built `layoffs_staging2` with row numbers for further cleaning.
- Removed remaining duplicates by filtering `row_num > 1`.

### STEP 8–10: Standardize Text Fields
- Trimmed whitespace from company names.
- Normalized industry labels (e.g., “Crypto” variations).
- Cleaned country names (removed trailing punctuation).

### STEP 11: Convert Dates
- Transformed string dates into proper `DATE` format using `STR_TO_DATE`.
- Altered column type to enforce consistency.

### STEP 12: Remove Invalid Records
- Deleted rows where both `total_laid_off` and `percentage_laid_off` were missing.

### STEP 13–14: Handle Missing Industry Values
- Used a self-join to fill missing industry values from matching company/location records.
- Converted empty strings to `NULL` for consistency.

### STEP 15: Final Cleanup
- Dropped helper column `row_num` after deduplication.
- Verified cleaned dataset with a final `SELECT`.

---

## 🛠 Techniques Used
- **Window Functions:** `ROW_NUMBER()` for duplicate detection  
- **CTEs:** Modular logic for deduplication  
- **String Functions:** `TRIM()`, `LIKE`, `TRAILING` for text normalization  
- **Date Conversion:** `STR_TO_DATE()` and column type enforcement  
- **Self-Join Imputation:** Filling missing industry values  
- **Defensive Cleaning:** Removing invalid records and normalizing empty strings  

---

## ✅ Outcome
The final dataset (`layoffs_staging2`) is:
- Deduplicated  
- Standardized across text fields  
- Converted to proper data types  
- Free of invalid records  
- Ready for exploratory analysis and visualization  

---

## 📌 Notes
- Raw data is preserved in `layoffs_staging` for reproducibility.  
- Cleaning steps are modular and can be rerun independently.  
- The workflow is scalable for larger datasets and adaptable to other domains.
