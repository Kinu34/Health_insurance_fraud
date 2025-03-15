
## Data Dictionary for Insurance Fraud Detection

### Beneficiaries Table
- **BeneID**: Unique identifier for the patient
- **DOB**: Date of birth
- **Gender**: Gender (M/F)
- **Race**: Racial classification
- **ChronicCond_Diabetes**: Indicates if patient has diabetes (True/False)

### Inpatient Claims Table
- **ClaimID**: Unique claim identifier
- **Provider**: ID of the provider (hospital/doctor)
- **BeneID**: ID of the patient
- **ClaimStartDt**: Date of claim initiation
- **InscClaimAmtReimbursed**: Amount claimed for the procedure
- **fraud_risk_score**: Assigned risk score (0-10)

### Outpatient Claims Table
- **ClaimID**: Unique claim identifier
- **InscClaimAmtReimbursed**: Amount claimed for outpatient services

### Providers Table
- **Provider**: Unique ID for providers
- **PotentialFraud**: Whether provider is suspected of fraud (True/False)
