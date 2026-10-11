# Healthcare-BI-Analysis-Power-BI-Dashboard
A 5-page Power BI report that analyses one year (Jan – Dec 2025) of patient-visit data from a multi-branch healthcare network in Nigeria. It covers revenue and profitability, patient demographics, hospital operations (waiting time, outcomes) and patient satisfaction, and ends with business insights and recommendations.

Business Objectives
Measure overall financial performance (revenue, cost, profit, margin).
Compare performance across states, branches and departments.
Understand who the patients are (age, gender, diagnosis, new vs. returning).
Find operational bottlenecks such as long waiting times and visit outcomes.
Evaluate payer mix (Self Pay, Private HMO, NHIA) and payment methods.
Compare actual revenue against annual state targets.
📂 Dataset
Table	Rows	Description
Patient_Visits	1,200 visits	Fact table: one row per visit (date, location, department, service, patient details, revenue, cost, waiting time, satisfaction, outcome)
State_Targets	4	Annual revenue target per state (Anambra ₦55M, Lagos ₦50M, Rivers ₦50M, Abuja ₦45M = ₦200M)
Patient_Table	1,200	Patient ID list
Date_Table	–	Calendar / helper table

Coverage: 1 Jan 2025 – 31 Dec 2025 · 4 states · 12 branches · 6 departments · 6 diagnoses · 3 insurance types · 4 payment methods.

Key columns in Patient_Visits: Patient_ID, Visit_Date, State, Branch, Department, Service, Age, Age Group, Gender, Diagnosis, Payment_Method, Insurance_Type, Visit_Count, Revenue_NGN, Cost_NGN, Waiting_Time_Min, Satisfaction_Score, Outcome, New/Returning.

🧹 Data Preparation (Power Query)
Imported the Excel workbook with Excel.Workbook and promoted headers.
Set correct data types (dates, whole numbers, decimals, text).
Created calculated columns:
Profit = Revenue_NGN − Cost_NGN
Margin = Profit / Revenue_NGN
Age Group (10-year bands)
Month, Month No., Quarter (from Visit_Date)
Built a one-to-many relationship: State_Targets[State] → Patient_Visits[State].
Removed blank/empty rows and checked data quality (see Data Quality Notes below).
🧮 DAX Measures
DAX
Total Revenue    = SUM(Patient_Visits[Revenue_NGN])
Total Cost       = SUM(Patient_Visits[Cost_NGN])
Total Profit     = SUM(Patient_Visits[Profit])
Profit Margin    = AVERAGE(Patient_Visits[Margin])
Total Visit      = DISTINCTCOUNT(Patient_Visits[Patient_ID])
Avg Visit count  = AVERAGE(Patient_Visits[Visit_Count])
AVG Wait Min.    = AVERAGE(Patient_Visits[Waiting_Time_Min])
Max Wait Time    = MAX(Patient_Visits[Waiting_Time_Min])
Avg Satisfaction = AVERAGE(Patient_Visits[Satisfaction_Score])
AVG AGE          = AVERAGE(Patient_Visits[Age])
📊 Report Pages
#	Page	What it shows
1	Patient Analysis (PA)	Total visits, average age, average satisfaction, visits by gender, age group, diagnosis, and new vs. returning patients per month. Slicers: Month, New/Returning
2	Executive Dashboard (ED)	KPI cards (Total Visits, Revenue, Profit, Profit Margin, Avg Wait), revenue by department, revenue & profit trend by month, revenue by insurance type, revenue & profit by state. Slicers: Department, Month
3	Hospital Operations (HO)	Visit trend, average waiting time by department and branch, max wait time, visit outcomes (Recovered / Follow-up / Admitted / Referred), average satisfaction. Slicers: New/Returning, Outcome
4	Financial Analysis (FA)	Revenue vs. cost vs. profit by month and department, profit by insurance type, payment-method split. Slicers: Insurance Type, Department
5	Insights / Recommendations	Written key insights and six recommendations

Design: green, white and gray colour theme on a 1920 × 1080 canvas.

🔍 Key Findings
Overall performance
1,200 visits generated ₦47.84M revenue against ₦29.50M cost, a profit of ₦18.35M (38.4% overall margin; the dashboard card shows 36.2% because it averages each visit's margin).
Average waiting time is 45.3 minutes (max 127 min). Average satisfaction is 3.71 / 5.
Geography
Rivers is the top state (₦12.73M, 26.6% of revenue); Anambra is lowest (₦11.33M).
The gap between top and bottom state is only ~12%, so performance is evenly spread.
Departments
Pediatrics is the top earner (₦9.39M, 19.6% of revenue) with the highest revenue per visit (₦42.5K) and margin (39.5%).
Pharmacy is the smallest contributor (₦7.51M).
Seasonality
Q3 was the peak quarter (₦13.55M, 336 visits).
Q4 revenue fell 19% below Q3 and had the lowest quarterly margin (37.3%). October revenue per visit dipped to ₦35.1K versus a ₦39.9K average.
Payer mix
Self Pay 48.3%, Private HMO 38.2%, NHIA 13.6% of revenue.
Margins are similar across payers (37.8% – 38.6%), so payer mix is not diluting profitability.
Targets
Revenue equals only 23.9% of the combined ₦200M annual state targets. Best attainment: Abuja (27.5%); lowest: Anambra (20.6%).
Patients & operations
Top diagnoses: Malaria (283), Typhoid (221), Hypertension (195).
Outcomes: 649 Recovered, 263 Follow-up, 155 Admitted, 133 Referred.
Slowest branches: Obio-Akpor (49.0 min), Ikeja (48.7 min), Wuse (46.8 min).
Satisfaction is lowest for ages 1–19 (3.47 – 3.59) and highest for 60+ (3.85+).
✅ Recommendations
Close the target gap – confirm whether the data is a full-year ledger or a sample; if complete, build a quarterly recovery plan for Anambra and Lagos and re-baseline unrealistic targets.
Cut waiting time – 25% of visits wait over 60 minutes (90th percentile: 78 min). Introduce triage and queue management at the slowest branches and adopt a 30-minute service standard.
Defend Q4 margin – review Q4 pricing and cost drivers and launch year-end check-up / wellness packages.
Grow insured business – expand NHIA / HMO partnerships and enrolment desks to reduce self-pay and collection risk.
Lift youth & paediatric experience – child-friendly spaces, shorter paediatric queues, better caregiver communication.
Fix data quality – validate department, gender and age capture (see below).
⚠️ Data Quality Notes
94 of 189 Maternity visits are recorded for male patients.
183 of 221 Pediatrics visits are for patients aged 18+.
The source sheet contains one blank trailing row, which was excluded from the analysis.
Profit Margin is calculated as the average of per-visit margins; the weighted margin (Total Profit ÷ Total Revenue) is 38.4%. Consider switching to DIVIDE([Total Profit],[Total Revenue]).
🛠️ Tools & Skills Demonstrated

Power BI Desktop · Power Query (M) · DAX · Data Modeling · Data Cleaning · KPI Design · Dashboard Storytelling · Business Insights

📁 Repository Structure
├── IFEXA-DA-0486-Health_Care_Dataset.pbix   # Power BI report
├── IFEXA_HealthCare_BI_Project_Dataset.xlsx # Source dataset
├── screenshots/                             # Dashboard images (add yours here)
└── README.md
▶️ How to Use
Download or clone this repository.
Open the .pbix file in Power BI Desktop.
If prompted, update the Excel data source path (Home → Transform data → Data source settings).
Use the slicers on each page to explore the data.
👤 Author

Your Name · Gerald B. Verallo

Readme
MD
Uploads
IFEXA-DA-0486-Health Care Dataset.pbix
Memory
Read · Healthcare Bi Powerbi Project
