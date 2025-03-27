
# Healthcare Provider Fraud Detection Analysis

## Project Overview
This project presents a comprehensive data analysis of healthcare provider fraud detection using real-world claims data. Healthcare fraud costs the industry billions of dollars annually, with estimates suggesting 3-10% of all healthcare spending is lost to fraud. This analysis demonstrates how data analytics techniques can be leveraged to identify suspicious billing patterns and potentially fraudulent providers.

The analysis utilizes SQLite for data storage and manipulation, pandas for data processing, and various visualization techniques to identify patterns indicative of fraudulent behavior. By analyzing relationships between different healthcare metrics, this project provides insights that could help insurance companies and regulatory bodies detect and prevent healthcare fraud.

# Project Structure
Capstone Project - HealthInsurance Fraud/
|- data/                                        # Raw CSV data files
|- env/                                         # Virtual environment
|- notebooks/                                   # Contains FinalCode.ipynb and UnitTestCode.ipynb
|- healthcare_fraud/                            # SQLite database
|-Healthcare_Provider_Fraud_Detection_README.md # This README file
|- requirements.txt                             # Python dependencies


## Features Implemented

### 1. Data Loading
- **Read TWO data files**: The project loads four CSV datasets (Beneficiary, Inpatient Claims, Outpatient Claims, and Provider data) containing healthcare information.

### 2. Data Cleaning and Operations
- **SQL join with data sets**: The project implements SQL joins between Provider data and Claims data, aggregating metrics at the provider level to facilitate fraud analysis.

### 3. Data Visualization
- **Multiple matplotlib/seaborn visualizations**: The project includes five detailed visualizations:
  - Distribution of fraudulent vs non-fraudulent providers
  - Average reimbursement comparison by claim type and fraud status
  - Distribution of total claim count by fraud status
  - Correlation heatmap of healthcare fraud features
  - Inpatient to outpatient ratio by fraud status

### 4. Best Practices
- **SQLite database implementation**: The project uses SQLite for efficient data processing and analysis, demonstrating knowledge of database integration.

- **Data dictionary**: The project analyzes multiple datasets related to healthcare claims and fraud detection. A comprehensive explanation of key variables and metrics is provided throughout the code via comments and analysis steps.

The datasets include:

Beneficiary Data: Patient demographics and health conditions

Inpatient Data: Claims submitted for hospital stays

Outpatient Data: Claims for outpatient services

Provider Data: Provider-level summary including fraud labels

# Key  Variables

| Column Name                     | Description                                                     |
|----------------------------------|-----------------------------------------------------------------|
| **Provider**                     | Unique ID for each healthcare provider                         |
| **InscClaimAmtReimbursed**       | Amount reimbursed for an insurance claim                        |
| **AdmissionDt, DischargeDt**     | Dates of hospital admission and discharge                       |
| **ClaimID**                      | Unique identifier for each claim                               |
| **BeneID**                       | Unique patient ID                                              |
| **DOB, DOD**                     | Date of birth and (if applicable) date of death                 |
| **ChronicCond_* **                | Binary flags indicating chronic conditions (e.g., heart failure)|
| **AttendingPhysician, OperatingPhysician, etc.** | Physician identifiers                           |
| **Fraud**                         | Label indicating if the provider is flagged for fraud (1=Yes, 0=No)|

Note: Additional derived columns like Age, ClaimDuration, TotalClaims, and AvgReimbursement are calculated during preprocessing and are documented in the respective code sections.

### 5. Data Interpretation
- **Annotated Jupyter Notebook**: The code includes detailed markdown cells explaining each step of the analysis, with clear explanations of methodologies and findings.

## Installation Instructions

### Required Libraries
- pandas
- numpy
- matplotlib
- seaborn
- sqlite3

### Setup Guide
1. Clone this repository:
```bash
git clone  https://github.com/Kinu34/Health_insurance_fraud.git
cd healthcare-fraud-detection
```

2. Create and activate a virtual environment (recommended):
```bash
# Using conda (recommended if you have Anaconda/Miniconda)
conda create -n fraud-detection python=3.9
conda activate fraud-detection

# OR using venv (built-in with Python)
python -m venv fraud-env

# On Windows
fraud-env\Scripts\activate

# On macOS/Linux
source fraud-env/bin/activate
```

3. Install required packages:
```bash
pip install pandas numpy matplotlib seaborn
```

4. Download and place the healthcare fraud datasets in a directory named `data/` within the project folder. Required files:
   - Beneficiarydata.csv
   - Inpatientdata.csv
   - Outpatientdata.csv
   - Providerdata.csv

## Usage
1. Open the Jupyter notebook:
```bash
jupyter notebook
```
2. Navigate to the notebooks/ folder and open the `FinalCode.ipynb` file.

3. Run all cells in sequence to reproduce the full analysis and visualizations.

Note: If you're running the notebook from the notebooks/ folder, the code uses a relative path to access the data/ folder located one level up (../data/).

## Testing

### Unit Tests

To ensure the correctness of the custom functions in this project, we've written unit tests using the `pytest` framework. These tests check the following functionalities:

1. **SQLite Table Creation** (`create_sqlite_tables`)
   - Verifies that the tables are correctly created in the SQLite database from the given data.
   
2. **Data Cleaning and Exploration** (`explore_and_clean`)
   - Ensures that missing values are handled properly and transformations (such as calculating age) are correctly applied.
   
3. **SQL Join and Data Aggregation** (`sql_join`)
   - Checks if the provider and inpatient data are joined accurately and that derived metrics like total claim counts and reimbursement totals are calculated as expected

### Running Unit Tests

Before running the unit tests, ensure that you have the required dependencies installed:

```bash
pip install pytest
pip install import-ipynb
```
#### Running Tests

These unit tests are implement inside the UnitTestCode.ipynb notebook. To run the tests:
1. Open the notebook in Jupyter.
2. Run each code cell in order.
3. The output of each test (pass/fail) will be shown after the very last cell code is run.

#### Example Output

In the notebook, each passing test looks like:

✅ Test 1: create_sqlite_tables PASSED!

### Test Coverage

The unit tests are written for the following functions:
- `create_sqlite_tables`: Tests the creation of tables in the SQLite database.
- `explore_and_clean`: Verifies the cleaning and preprocessing of data.
- `sql_join`: Confirms that SQL joins and aggregations are performed correctly.


## Data Dictionary

### Key Datasets
- **Beneficiarydata**: Patient demographics and coverage information
  - `DOB`: Date of Birth
  - `DOD`: Date of Death (if applicable)
  - `Gender`: Patient gender
  - `Race`: Patient race/ethnicity
  - `State/County`: Geographic location

- **Inpatientdata**: Hospital admission claims and procedures
  - `ClaimID`: Unique identifier for the claim
  - `Provider`: Healthcare provider identifier
  - `ClaimStartDt/ClaimEndDt`: Claim period dates
  - `AdmissionDt/DischargeDt`: Hospital stay dates
  - `InscClaimAmtReimbursed`: Amount reimbursed by insurance
  - `DeductibleAmtPaid`: Deductible amount paid by patient
  - `LengthOfStay`: Calculated days of hospitalization

- **Outpatientdata**: Ambulatory and clinical visit claims
  - `ClaimID`: Unique identifier for the claim
  - `Provider`: Healthcare provider identifier
  - `ClaimStartDt/ClaimEndDt`: Claim period dates
  - `InscClaimAmtReimbursed`: Amount reimbursed by insurance
  - `DeductibleAmtPaid`: Deductible amount paid by patient

- **Providerdata**: Healthcare provider information with fraud labels
  - `Provider`: Unique provider identifier
  - `PotentialFraud`: Yes/No indicator of fraud
  - `Fraud`: Binary indicator (1=Yes, 0=No)

### Derived Metrics
- `InpatientClaimCount`: Number of inpatient claims per provider
- `OutpatientClaimCount`: Number of outpatient claims per provider
- `AvgInpatientReimbursement`: Average reimbursement for inpatient claims
- `AvgOutpatientReimbursement`: Average reimbursement for outpatient claims
- `TotalReimbursement`: Sum of inpatient and outpatient reimbursements
- `AvgLengthOfStay`: Average hospital stay duration
- `InpatientToOutpatientRatio`: Ratio of inpatient to outpatient claims

## Key Findings

The analysis revealed several patterns consistent with healthcare fraud:

1. **Billing Anomalies**: Fraudulent providers show systematically higher average reimbursement amounts, particularly for inpatient services.

2. **Volume Discrepancies**: There are statistically significant differences in claim volumes between fraudulent and legitimate providers.

3. **Length of Stay Manipulation**: Fraudulent providers demonstrate unusual patterns in patient length of stay, potentially indicating upcoding or unnecessary hospitalization.

4. **Service Mix Red Flags**: The ratio between inpatient and outpatient claims serves as a powerful indicator of potential fraud.

5. **Reimbursement Tier Analysis**: Fraud patterns vary significantly across reimbursement categories, with distinct patterns in the highest reimbursement tiers.

## Future Enhancement Opportunities

This analysis framework could be enhanced through:

- **Machine Learning Integration**: Predictive models to score providers by fraud risk
- **Network Analysis**: Examining provider-patient-facility relationships for collusion patterns
- **Temporal Pattern Detection**: Time-series analysis to identify evolving fraud schemes
- **Natural Language Processing**: Analysis of procedure descriptions and notes for upcoding evidence
- **Geographic Hotspot Analysis**: Spatial clustering to identify regional fraud patterns

## AI Assistance
This project was developed with support from AI tools such as ChatGPT, which was used for troubleshooting, debugging and improving documentation.


## Author
[Kinu Patel]

## Acknowledgments
- Data source citation: https://pmc.ncbi.nlm.nih.gov/articles/PMC2410006/
- Code:You Data Analysis Capstone Project (August 2024 Cohort)
