
# Requirements:
1. KPIs and Trends: Identify and present the key 
performance indicators (KPIs) and significant trends in the 
dataset.

2. Detailed Analysis: Ensure the analysis is thorough and 
detailed, covering all relevant aspects of the healthcare 
center's finance and the performance of healthcare 
providers.

3. Dashboard Creation: Create a comprehensive 
dashboard consisting of 3 to 4 pages that includes:
 - Financial Overview: Summarize the financial health of 
the healthcare center.
 - Provider Insights: Analyze the performance and 
efficiency of healthcare providers.
 - Trend Analysis: Highlight any important trends over 
time.
 - Additional Insights: Any other relevant insights that can 
be derived from the data


# Cleaning Data and do EDA
## How to Add table Date:

DateTable = 
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "mmm"),
    "Monthnum", MONTH([Date]),
    "Weekday", FORMAT([Date], "ddd"),
    "Weeknum", WEEKNUM([Date]),
    "Qtr", "Q-" & FORMAT([Date], "Q"),
    "Weektype", IF(WEEKDAY([Date]) = 1 || WEEKDAY([Date]) = 7, "Weekend", "Weekday")
)

## Basic Measures used in Dashboard
Billing Amount: Total Billing Amount = [Total Medication Cost]+ [Total Room Charges]+[Total Treatment Cost]

Medication Cost: Total Medication Cost = SUM(visits[Medication Cost])

Treatment Cost: Total Treatment Cost = SUM(visits[Treatment Cost])

Total Insurance: Total Insurance Covered = SUM(visits[Insurance Coverage])

Length of Stay= DATEDIFF(visits[Admitted Date], visits[Discharge Date], DAY

Room Charges: Total Room Charges = SUMX(visits,visits[Room Charges(daily rate)] * visits[Length of Stay])


Out-of-Pocket: Out-of-Pocket = [Total Billing Amount] - [Total Insurance Covered]

Total Patients = DISTINCTCOUNT(visits[Patient ID])


All Billing Amount = DIVIDE([Total Billing Amount], CALCULATE([Total Billing Amount], ALL(procedures[Procedure])))


## Average Mearures
Average Billing Amount per visit = DIVIDE([Total Billing Amount], [Total Patients], 0)

Average Insurance Covered = AVERAGE(visits[Insurance Coverage])

Average Medication Cost = AVERAGE(visits[Medication Cost])

Average Out-of-Pocket = DIVIDE([Out-of-Pocket], [Total Patients], 0)

Average Patient Satisfaction Score = AVERAGE(visits[Patient Satisfaction Score])

Average Treatment Cost = AVERAGE(visits[Treatment Cost])

Avererage Length of Stay = AVERAGE(visits[Length of Stay])

Average Room Charge = DIVIDE([Total Room Charges], [Total Patients], 0)


## Financial Insights
### Billing Amounts:

The Total Billing Amount across different cities shows a significant variation, with some cities like Birmingham and Edinburgh having higher totals compared to others like Bristol and Leeds.

Similarly, the Total Billing Amount by Procedure reveals that procedures like MRI Scans and CT Scans contribute more to the total billing compared to X-Rays and Blood Tests.

### Average Costs:

The Average Out-of-Pocket Cost is $259, which indicates the typical amount a patient might need to pay from their own funds.
The Average Billing Amount per Visit is $711, showing the general cost incurred for a single healthcare visit.

Average Insurance Covered is $457, providing insight into how much insurance typically covers for the patients.

Average Medication Cost is $108, which is the average cost patients spend on medications.

Average Room Charge is $74, indicating the typical cost for room charges.

Average Treatment Cost is $528, reflecting the average cost associated with treatments.

### Service and Procedure Insights
**Procedure Costs:**

There is a substantial difference in billing amounts among different procedures. For instance, MRI Scans have a much higher billing total compared to procedures like Ultrasounds and Blood Tests.

**Departmental Billing:**

Departments like Neurology and Cardiology have higher total billing amounts ($0.48M and $0.17M respectively) compared to other departments like General Surgery and Pediatrics.

### Diagnostic and Service Type Insights

**Billing by Diagnosis and Service Type:**

There are differences in the total billing amount by diagnosis and service type. For example, conditions like Migraine and Asthma have different billing patterns, with Migraine showing a higher percentage for Emergency services.

The service types (Emergency, Inpatient, Outpatient) also show varied billing distributions across different diagnoses. For instance, Hypertension has a higher percentage of Inpatient services compared to Fracture, which has a higher Emergency service percentage.

### Demographic Insights
**Racial Breakdown:**

The data includes breakdowns by race, which can be analyzed further to understand disparities or differences in billing amounts, access to care, and insurance coverage among different racial groups.

These insights can help healthcare administrators and policymakers make informed decisions about resource allocation, cost management, and addressing disparities in healthcare services. They also provide valuable information for improving patient care and financial planning within healthcare institutions.

![image](https://github.com/Thuhien23/Healthcare-analysis/assets/96719464/e3e8d67a-36c2-447d-b384-6e6b48885b07)
