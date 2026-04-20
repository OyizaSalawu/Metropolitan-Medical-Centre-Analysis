  Metropolitan-Medical-Centre-Analysis

This project provides an end-to-end Exploratory Data Analysis (EDA) of hospital operational data. Using Python, I analyzed patient demographics, departmental revenue, and clinical outcomes to identify the primary drivers of hospital charges and patient satisfaction.

   📊 Project Highlights
Revenue Analysis: Identified Cardiology and General Surgery as the primary revenue drivers.
Financial Modeling: Engineered features to calculate `Insurance_Coverage` vs. `Out_of_Pocket` expenses.
Operational Bottlenecks: Analyzed the impact of `Admission_Type` (Emergency vs. Elective) on wait times and total charges.
Satisfaction Drivers: Used statistical grouping to see if `Staff_to_Patient_Ratio` impacted `Satisfaction_Scores`.


  💻 Key Technical Implementation

Below are the core Python techniques used in the analysis:

 1. Data Cleaning & Imputation
Handling missing values in sensitive medical data to ensure statistical accuracy.
```python
# Filling missing satisfaction scores with the mean to maintain dataset size
hospital_data['Patient_Satisfaction_Score'].fillna(hospital_data['Patient_Satisfaction_Score'].mean(), inplace=True)
```

  2. Departmental Financial Aggregation
Comparing how different departments perform in terms of revenue and length of stay.
```python
# Grouping by Department to analyze financial and operational metrics
dept_analysis = hospital_data.groupby('Department').agg({
    'Total_Charges': 'sum',
    'Length_of_Stay_Days': 'mean',
    'Patient_Satisfaction_Score': 'mean'
}).sort_values(by='Total_Charges', ascending=False)
```

 3. Patient Satisfaction Categorization
Using `pd.cut` to bin continuous wait times into discrete categories for clearer visualization.
```python
wait_bins = [0, 2, 4, 12]
wait_labels = ['≤2hrs', '2-4hrs', '>4hrs']

hospital_data['Wait_Time_Category'] = pd.cut(hospital_data['Wait_Time_Hours'], bins=wait_bins, labels=wait_labels)
```

---

   📈 Key Findings
1. Length of Stay: Confirmed as the #1 driver of total hospital charges across all departments.
2. Emergency Admissions: Result in **35% higher average charges and significantly longer wait times compared to Elective admissions.
3. Insurance Coverage: Medicaid and Medicare patients saw the highest average out-of-pocket costs in specialized surgical departments.



   🛠 Tools Used
 Python
   Pandas: Data manipulation and feature engineering.
   Matplotlib: Advanced data visualization and departmental comparisons.

 
