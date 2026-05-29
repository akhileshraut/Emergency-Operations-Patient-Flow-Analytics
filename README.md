# Pharmacy-Profitability-Analytics

Code Blue — Healthcare Analytics · Full Data Dictionary	Unnamed: 1	Unnamed: 2	Unnamed: 3	Unnamed: 4	Unnamed: 5

Table	Column Name	Data Type	Description	UK Context / Sample Values	Notes

Dim_Hospital	Hospital_ID	Text	Unique hospital identifier	H01 … H11	Primary key

Dim_Hospital	Hospital_Name	Text	Real UK hospital name	King's College Hospital NHS FT	—

Dim_Hospital	Archetype	Text	Operational profile for benchmarking	Large Urban Trauma Center, Rural Community Hospital …	8 archetypes

Dim_Hospital	NHS_Trust_Type	Text	NHS organisational classification	NHS Foundation Trust / NHS Trust / Independent / Private	UK-specific

Dim_Hospital	Region_ID	Text	Links to Dim_Region	R01 … R06	FK → Dim_Region

Dim_Hospital	City	Text	UK city of hospital	London, Bristol, Leeds …	—

Dim_Hospital	Beds	Integer	Total licensed inpatient beds	145 … 850	NHS England average DGH ~400

Dim_Hospital	ICU_Beds	Integer	Dedicated ICU / HDU beds	12 … 80	NHS avg ~8 ICU per 100 beds

Dim_Hospital	ED_Bays	Integer	Emergency department treatment bays	10 … 48	—

Dim_Hospital	Annual_Budget_M	Decimal	Annual operating budget (£ millions)	58 … 420	NHS FT range: £60M–£1.5B

Dim_Hospital	Staff_FTE	Integer	Total full-time equivalent staff headcount	420 … 2,800	—

Dim_Hospital	Founding_Year	Integer	Year hospital was established	1888 … 2009	—

Dim_Hospital	Teaching_Hospital	Boolean	Whether hospital has undergraduate teaching mandate	True / False	—

Dim_Hospital	Trauma_Level	Integer	Major Trauma Centre designation (1 = MTC, 4 = non-trauma)	1 … 4	NHS England MTC network

Dim_Hospital	Private	Boolean	Independent / private (not NHS-funded) hospital	True / False	H02 Nuffield, H08 Spire

Dim_Hospital	Avg_Daily_Admissions_Base	Integer	Baseline daily admissions (2022 reference year)	42 … 310	Grows with Growth_Trend

Dim_Hospital	Satisfaction_Base	Integer	Baseline Friends & Family Test score (0–100)	52 … 91	NHS FFT benchmark ~75

Dim_Hospital	Efficiency_Score	Decimal	Operational efficiency index (0 = poor, 1 = excellent)	0.55 … 0.94	Internal benchmarking metric

Dim_Hospital	Cost_Index	Decimal	Cost per patient relative to network average (1.0 = average)	0.72 … 1.95	—

Dim_Hospital	Readmission_Rate_Base	Decimal	Baseline 30-day emergency readmission rate	0.048 … 0.218	NHS England target < 11%

Dim_Hospital	Staffing_Stress	Text	Staffing pressure classification affecting burnout & delays	LOW / MODERATE / HIGH / CRITICAL	—

Dim_Hospital	Growth_Trend	Decimal	Annual compound admissions growth rate	0.01 … 0.05	—

Dim_Hospital	Quality_Trend	Decimal	Annual quality change (+ve = improving, -ve = declining)	-0.025 … 0.012	—

Dim_Hospital	Special_Profile	Text	Analytical profile tag for benchmarking scenarios	HIGH_VOLUME_LOW_SATISFACTION, IMPROVING_OVER_TIME …	10 distinct profiles

Dim_Hospital	Latitude	Decimal	Hospital geographic latitude (WGS84)	50.27 … 53.99	For map visuals in Power BI

Dim_Hospital	Longitude	Decimal	Hospital geographic longitude (WGS84)	-5.05 … 1.22	For map visuals in Power BI

Dim_Region	Region_ID	Text	Unique region identifier	R01 … R06	Primary key

Dim_Region	Region_Name	Text	Real UK NHS region name	Greater London, West Midlands …	ONS region boundaries

Dim_Region	Population_M	Decimal	Regional population in millions	5.5 … 9.2	ONS 2023 mid-year estimates

Dim_Region	Urban_Rural	Text	ONS urbanisation classification	Urban / Suburban / Rural / Mixed	—

Dim_Region	Avg_Income_K	Integer	Average household income (£ thousands)	27 … 42	ONS regional income statistics

Dim_Region	Elderly_Pct	Decimal	Percentage of population aged 65+	12.1 … 20.1	Higher in rural regions

Dim_Region	Poverty_Rate	Decimal	Regional relative poverty rate	0.098 … 0.198	JRF poverty statistics proxy

Dim_Department	Department_ID	Text	Unique department identifier	D01 … D12	Primary key

Dim_Department	Department_Name	Text	Clinical department name	Emergency Department, ICU, Cardiology …	12 departments

Dim_Department	Type	Text	Department operational category	Emergency / Critical Care / Inpatient / Elective	—

Dim_Department	ICU_Capable	Boolean	Department can manage level 2/3 (ICU/HDU) patients	True / False	NHS level 2 = HDU, level 3 = ICU

Dim_Date	Date_Key	Integer	Surrogate date key in YYYYMMDD format	20240101	Use for joins from fact tables

Dim_Date	Full_Date	Date	Calendar date	2024-01-01	Mark as Date Table in Power BI

Dim_Date	Year	Integer	Calendar year	2024, 2025	—

Dim_Date	Quarter	Text	Financial quarter label	Q1 … Q4	NHS financial year starts April

Dim_Date	Month	Integer	Month number	1 … 12	—

Dim_Date	Month_Name	Text	Full month name	January … December	—

Dim_Date	Week_Number	Integer	ISO 8601 week of year	1 … 53	—

Dim_Date	Day_of_Week	Text	Full day name	Monday … Sunday	—

Dim_Date	Day_Number	Integer	Day number (0 = Monday, 6 = Sunday)	0 … 6	Python/ISO convention

Dim_Date	Is_Weekend	Boolean	Saturday or Sunday	True / False	ED demand shifts at weekends

Dim_Date	Is_Holiday	Boolean	UK public holiday	True / False	Bank holidays included

Dim_Date	Season	Text	Calendar season	Spring / Summer / Autumn / Winter	—

Dim_Date	Is_Winter	Boolean	December, January, February	True / False	Key respiratory pressure driver

Dim_Date	Is_Flu_Season	Boolean	November through March	True / False	PHE definition

Dim_Patient	Patient_ID	Text	Unique anonymised patient identifier	P0000001 … P0180000	Synthetic — not real patients

Dim_Patient	Age	Integer	Patient age in years	0 … 95	—

Dim_Patient	Gender	Text	Patient gender	Male / Female / Non-binary	—

Dim_Patient	Income_Annual	Integer	Estimated annual household income (£)	12,000 … 250,000	Synthetic estimate

Dim_Patient	Income_Segment	Text	Income band classification	Low / Low-Middle / Middle / High	—

Dim_Patient	Insurance_Type	Text	NHS or private coverage type	NHS Funded / NHS Continuing Care / Private Insurance / Self-Pay	UK NHS terminology

Dim_Patient	Primary_Hospital_ID	Text	Patient's primary registered hospital	H01 … H11	FK → Dim_Hospital

Dim_Patient	Chronic_Conditions	Text	Active long-term conditions (semicolon-separated)	Hypertension; Diabetes Type 2	None = no chronic conditions

Dim_Patient	Chronic_Condition_Count	Integer	Number of active chronic conditions	0 … 3	LTC count per NHS QOF

Dim_Patient	Risk_Category	Text	Clinical risk stratification	Low / Medium / High / Critical	NHS risk stratification framework

Dim_Patient	Postcode_District	Text	Anonymised UK postcode district	SE5, LS1, BS3 …	Real UK district codes

Dim_Doctor	Doctor_ID	Text	Unique doctor identifier	DR00001 … DR01800	Primary key

Dim_Doctor	Doctor_Name	Text	Full name (synthetic)	Dr. Sarah Johnson	Synthetic — not real individuals

Dim_Doctor	Specialty	Text	GMC-registered clinical specialty	Emergency Medicine, Cardiology, Geriatrics …	15 specialties

Dim_Doctor	Grade	Text	NHS medical grade / seniority	Consultant / Senior Registrar / Registrar / SHO / FY2 / FY1	NHS Agenda for Change

Dim_Doctor	Years_Experience	Integer	Total years of clinical practice	0 … 35	—

Dim_Doctor	Primary_Hospital_ID	Text	Home hospital	H01 … H11	FK → Dim_Hospital

Dim_Doctor	Annual_Salary	Integer	Annual salary (£) per NHS pay scales	£29K–£144K	Based on 2024/25 NHS pay bands

Dim_Doctor	Part_Time_Flag	Boolean	Less than full WTE contract	True / False	~12% of NHS medical workforce

Dim_Doctor	Burnout_Baseline	Decimal	Individual baseline burnout propensity score (0–1)	0.20 … 0.70	GMC NTS-inspired metric

Dim_Diagnosis	Diagnosis_ID	Text	Unique diagnosis category identifier	DX01 … DX15	Primary key

Dim_Diagnosis	Category	Text	ICD-10 clinical category name	Cardiovascular, Respiratory, Trauma/Injury …	—

Dim_Diagnosis	ICD_Chapter	Text	ICD-10 chapter code	I, J, S-T, K, G …	WHO ICD-10 coding

Dim_Diagnosis	Severity_Weight	Decimal	Average clinical severity (0 = mild, 1 = life-threatening)	0.35 … 0.95	Used to generate Severity_Level

Dim_Diagnosis	ICU_Probability	Decimal	Probability case requires ICU/HDU admission	0.02 … 0.32	—

Dim_Diagnosis	Avg_LOS_Hours	Integer	Average length of stay in hours	24 … 144	NHS Reference Costs basis

Dim_Diagnosis	Readmission_Risk	Text	30-day readmission risk tier	LOW / MEDIUM / HIGH	NHS CQUIN readmission indicator

Dim_Diagnosis	Cost_Weight	Decimal	Relative treatment cost vs network average (1.0 = average)	0.75 … 2.20	NHS National Tariff proxy

Fact_Patient_Visits	Visit_ID	Text	Unique visit / attendance identifier	V04000001 …	Primary key. Prefix V04/V05 = year

Fact_Patient_Visits	Patient_ID	Text	Attending patient	P0000001 …	FK → Dim_Patient

Fact_Patient_Visits	Hospital_ID	Text	Hospital where attendance occurred	H01 … H11	FK → Dim_Hospital

Fact_Patient_Visits	Department_ID	Text	Receiving clinical department	D01 … D12	FK → Dim_Department

Fact_Patient_Visits	Doctor_ID	Text	Responsible clinician	DR00001 …	FK → Dim_Doctor

Fact_Patient_Visits	Arrival_DateTime	DateTime	Date and time patient arrived (rounded to minute)	2024-01-01 08:42	Use DATE() in Power BI for Dim_Date join

Fact_Patient_Visits	Triage_DateTime	DateTime	Date and time triage was completed	2024-01-01 09:05	~2% missing — delayed triage records

Fact_Patient_Visits	Treatment_Start_DateTime	DateTime	Date and time treatment began	2024-01-01 09:48	~1.5% missing

Fact_Patient_Visits	Discharge_DateTime	DateTime	Date and time patient was discharged	2024-01-02 11:20	~2.5% missing

Fact_Patient_Visits	Admission_Type	Text	How patient entered the system	Emergency / Urgent / Elective / Transfer	NHS SUS submission categories

Fact_Patient_Visits	Severity_Level	Integer	Clinical severity score (1 = minor, 5 = critical)	1 … 5	Based on NHS NEWS2 acuity bands

Fact_Patient_Visits	Diagnosis_Category	Text	Primary diagnosis category code	DX01 … DX15	FK → Dim_Diagnosis

Fact_Patient_Visits	Length_of_Stay_Hours	Decimal	Total hours from arrival to discharge	1.0 … 500+	NHS target: ED < 4hrs

Fact_Patient_Visits	Wait_Time_Minutes	Integer	Minutes from arrival to start of treatment	8 … 800+	Key NHS ED KPI

Fact_Patient_Visits	Treatment_Delay_Minutes	Integer	Minutes from triage completion to treatment start	5 … 960	Component of overall wait

Fact_Patient_Visits	ICU_Required_Flag	Boolean	Patient required ICU or HDU level care	True / False	NHS level 2/3 critical care

Fact_Patient_Visits	Outcome	Text	Clinical outcome at discharge	Discharged / Admitted / Transferred / Deceased / AMA	NHS ECDS outcome codes

Fact_Patient_Visits	Mortality_Flag	Boolean	Patient died during this attendance	True / False	~3.2% network rate

Fact_Patient_Visits	Readmission_30_Days_Flag	Boolean	Emergency readmission within 30 days	True / False	NHS CQUIN indicator

Fact_Patient_Visits	Insurance_Type	Text	Coverage type at time of attendance	NHS Funded / NHS Continuing Care / Private Insurance / Self-Pay	Snapshot — may differ from Dim_Patient

Fact_Patient_Visits	Treatment_Cost	Decimal	Total treatment cost in £	£250 … £95,000+	Based on NHS National Tariff

Fact_Patient_Visits	Revenue_Amount	Decimal	Revenue received for this attendance (£)	£100 … £128,000+	Cost × coverage multiplier

Fact_Patient_Visits	Satisfaction_Score	Decimal	Patient-reported experience score (0–100)	10 … 100	Proxy for NHS Friends & Family Test. ~3% missing

Fact_Patient_Visits	Complaint_Flag	Boolean	Formal written complaint submitted	True / False	~8–15% of low-satisfaction visits

Fact_Patient_Visits	Ambulance_Arrival_Flag	Boolean	Patient arrived by NHS ambulance	True / False	~48% of emergency attendances

Fact_Patient_Visits	Hospital_Name	Text	Real UK hospital name (denormalised for convenience)	King's College Hospital NHS FT	Matches Dim_Hospital.Hospital_Name

Fact_Patient_Visits	Latitude	Decimal	Hospital latitude — enables map visuals directly from fact	51.4683	No join required for mapping

Fact_Patient_Visits	Longitude	Decimal	Hospital longitude — enables map visuals directly from fact	-0.0942	No join required for mapping

Fact_Staffing	Shift_ID	Text	Unique shift record identifier	SH010000001 …	Primary key

Fact_Staffing	Hospital_ID	Text	Hospital for this shift	H01 … H11	FK → Dim_Hospital

Fact_Staffing	Department_ID	Text	Department for this shift	D01 … D12	FK → Dim_Department

Fact_Staffing	Shift_Date	Date	Calendar date of shift	2024-01-01	FK → Dim_Date (Full_Date)

Fact_Staffing	Shift_Type	Text	Time band of shift	Morning / Afternoon / Night	Three shifts per department per day

Fact_Staffing	Doctors_On_Duty	Integer	Doctors rostered and present on shift	0 … 8	Excludes absent staff

Fact_Staffing	Nurses_On_Duty	Integer	Nurses rostered and present on shift	0 … 22	—

Fact_Staffing	Support_Staff_Count	Integer	Healthcare assistants and support staff on shift	0 … 10	—

Fact_Staffing	Staff_Absence_Count	Integer	Staff who were absent or called in sick	0 … 18	Zero ghost shifts — all rows have ≥1 staff

Fact_Staffing	Overtime_Hours	Decimal	Total overtime hours worked on this shift	0 … 40+	Spikes during winter and anomaly events

Fact_Staffing	Staff_Cost	Decimal	Total labour cost for shift (£)	£200 … £48,000	Includes overtime premium. Inflates ~3.3% p.a.

Fact_Staffing	Burnout_Risk_Index	Decimal	Composite staff burnout risk score (0 = none, 1 = critical)	0.0 … 1.0	Rising YoY at underfunded hospitals

Fact_Staffing	Hospital_Name	Text	Real UK hospital name (denormalised)	King's College Hospital NHS FT	Matches Dim_Hospital.Hospital_Name

Fact_Staffing	Latitude	Decimal	Hospital latitude	51.4683	For geographic filtering

Fact_Staffing	Longitude	Decimal	Hospital longitude	-0.0942	For geographic filtering

Fact_Financials	Financial_Record_ID	Text	Unique monthly financial record	FIN000001 …	Primary key

Fact_Financials	Hospital_ID	Text	Hospital	H01 … H11	FK → Dim_Hospital

Fact_Financials	Year	Integer	Financial year	2024, 2025	NHS financial year April–March

Fact_Financials	Month	Integer	Calendar month number	1 … 12	—

Fact_Financials	Visit_Count	Integer	Total patient attendances in month	500 … 18,000	—

Fact_Financials	Operational_Cost	Decimal	Total monthly operational expenditure (£)	£500K … £12M	—

Fact_Financials	Staffing_Cost	Decimal	Monthly labour cost component (£)	£200K … £8M	Largest single cost driver

Fact_Financials	Emergency_Department_Cost	Decimal	ED-specific monthly cost (£)	£80K … £4M	~38% of treatment cost

Fact_Financials	ICU_Cost	Decimal	Monthly ICU/HDU bed cost (£)	£50K … £3M	~£1,850 per ICU day

Fact_Financials	Revenue	Decimal	Total monthly revenue received (£)	£300K … £14M	NHS National Tariff + private income

Fact_Financials	Profit_Margin	Decimal	(Revenue + Funding − Cost) ÷ Total Income	-0.18 … 0.22	NHS FTs typically -5% to +5%

Fact_Financials	Government_Funding	Decimal	Monthly NHS block/grant funding (£)	£0 (private) … £8.7M	~2% missing — delayed reporting

Fact_Financials	Equipment_Investment	Decimal	Capital equipment spend that month (£)	£0 … £5.2M	~3% missing; spikes on expansion events

Fact_Financials	Expansion_Projects_Flag	Boolean	Major capital project active this month	True / False	—

Fact_Financials	Bed_Occupancy_Rate	Decimal	Average bed occupancy rate (>1.0 = over capacity)	0.35 … 1.05	NHS target < 85%

Fact_Financials	Avg_Patient_Satisfaction	Decimal	Monthly average patient experience score (0–100)	20 … 95	NHS FFT proxy

Fact_Financials	Readmission_Rate	Decimal	Monthly 30-day emergency readmission rate	0.04 … 0.42	NHS target < 11%

Fact_Financials	Complaint_Rate	Decimal	Proportion of attendances generating formal complaint	0.005 … 0.042	NHS average ~0.8%

Fact_Financials	Mortality_Rate	Decimal	In-hospital mortality rate for the month	0.01 … 0.08	HSMR proxy

Fact_Financials	Avg_Wait_Time_Minutes	Decimal	Average patient wait time in minutes	30 … 180+	NHS 4-hour standard: < 240 min

Fact_Financials	Total_Overtime_Hours	Decimal	Total overtime hours across all departments	50 … 3,500	Rising during winter peaks

Fact_Financials	Avg_Burnout_Index	Decimal	Average staff burnout index across all shifts	0.20 … 0.95	GMC NTS-inspired proxy

Fact_Financials	Total_Staff_Absences	Integer	Total staff absences across all shifts in month	50 … 1,800	Includes sickness and unauthorised

Fact_Financials	Hospital_Name	Text	Real UK hospital name (denormalised)	King's College Hospital NHS FT	Convenience column for visuals

Fact_Financials	Latitude	Decimal	Hospital latitude	51.4683	For geographic analysis

Fact_Financials	Longitude	Decimal	Hospital longitude	-0.0942	For geographic analysis

