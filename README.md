VoltRelay Energy Analytics
Operational Performance, Customer Retention, and Business Insights
Individual Data Analytics Hackathon Submission
Author: Fatima Jaffar
Analysis period: January 2024 – June 2025
Scope: 6 Indian cities | 152 stations
Dataset type: Synthetic
Project Overview
This project investigates the operational and business performance of VoltRelay, a simulated electric-vehicle (EV) battery-swapping network operating across six Indian cities.

The central business question is:
How can a rapidly growing battery-swapping network improve operational reliability while maintaining customer retention and sustainable unit economics?

The analysis examines swap activity, station-level battery availability, customer support, rider retention, infrastructure segments, and an estimated contribution-per-swap proxy.
Project Resources
- Google Drive folder (Colab notebook and dashboard files):
  https://drive.google.com/drive/folders/14saHjZfNORRn8F__qBTsfG3DATiInwGF?usp=sharing
- Full analytical report (PDF): Add the direct, viewable PDF link here.
- Google Colab notebook: Add the direct notebook link here, if available.
Make sure shared links are accessible to reviewers. The Drive folder link is a resource folder, not a direct link to an individual notebook or PDF.
Tools and Technologies
- Python
- Pandas and NumPy
- DuckDB
- Matplotlib
- Google Colab
- SQL for analytical queries
Datasets
The project uses eight synthetic relational datasets:
Dataset	Records	Main contents
Swap events	3,877,013	Swap attempts, outcomes, timestamps, battery readings, tariffs, recorded revenue
Station hourly status	1,487,712	Hourly telemetry, minimum battery availability, charging and outage indicators
Support tickets	44,000	Complaint categories, resolution status, resolution time, and CSAT
Riders	20,000	Signup cohorts, customer channel, plan, vehicle class, and city
Batteries	6,500	Battery specifications and lifecycle metadata
City daily context	3,282	Weather, disruptions, holidays, and city-level context
Stations	152	City, zone, location, charger generation, and station operating costs
Fleet partners	12	Partner contracts, discounts, and billing terms


Data note: The datasets are synthetic. Results describe patterns within this dataset and should not be interpreted as verified performance of a real company or market.
Methodology
1. Inspected dataset schemas, record counts, key fields, and relationships.
2. Standardized city names and selected categorical values.
3. Validated primary-key uniqueness and foreign-key integrity.
4. Created non-destructive data-quality flags for questionable records and missing values.
5. Analyzed business growth and unsuccessful swap events over time.
6. Compared operational performance across cities, stations, charger generations, and expansion waves.
7. Joined swap events to hourly station-status records to examine battery availability.
8. Evaluated support-ticket patterns and complete 2024 rider cohorts.
9. Estimated a contribution-per-completed-swap proxy and checked recorded revenue against list price - discount.
10. Translated findings into prioritized operational and financial recommendations.
Data-quality approach
All eight datasets retained their original row counts. Questionable values were flagged rather than silently deleted or imputed.

Important limitations identified include:
- 17,557 swap records with numerical anomalies, including out-of-range SOC/SOH values or negative distance.
- 5,154 batteries with lifecycle-date inconsistencies affecting 1,659,371 events; battery age analysis was therefore excluded.
- 9,384 station-hour records with missing telemetry status.
- 818,160 structurally missing 3W availability observations at stations not configured for 3W swapping.
- 28,871 support tickets with missing CSAT values.
Key Findings
1. Growth outpaced reliability
- Total swap events: 3,877,013
- Completed swaps: 3,645,809
- Overall unsuccessful event rate: 5.96%
- Monthly completed swaps increased from 105,490 in January 2024 to 307,259 in June 2025 (approximately 2.91×).
- Monthly unsuccessful event rate increased from 4.40% to 8.55% over the same comparison.
Unsuccessful events include no-charged-battery failures, abandoned queues, rider cancellations, and system errors. They should not all be described as technical failures.
2. Reliability differed by city
City	Unsuccessful event rate	No-battery failure rate
Jaipur	7.85%	4.78%
Delhi NCR	7.35%	4.41%
Hyderabad	6.69%	3.97%
Pune	4.99%	2.80%
Bengaluru	4.56%	2.50%
Mumbai	4.45%	2.42%


Jaipur, Delhi NCR, and Hyderabad are priority markets for further operational investigation.
3. Battery availability was associated with no-battery failures
- Station-hours with zero available batteries: 7.21% no-battery failure rate.
- Station-hours with six or more available batteries: 3.25% no-battery failure rate.
This is an observational association. Hourly minimum inventory is not the exact battery count at the moment of each swap, so it does not establish causation.
4. Evening failure activity was elevated
No-battery failure rates were elevated between 7 PM and 10 PM, ranging from 3.91% to 3.95%. This supports reviewing pre-evening charging buffers, redistribution, and monitoring.
5. Month 3 retention differed by vehicle class
Across the evaluated 2024 cohorts:
- 2W segment Month 3 retention ranged from 78.38% to 80.42%.
- 3W segment Month 3 retention ranged from 73.27% to 77.53%.
The pattern is observational and some 3W segments have relatively small cohort sizes. It warrants further investigation rather than a causal conclusion.
6. Contribution proxy improved, but revenue needs reconciliation
The estimated contribution proxy per completed swap improved from -₹7.95 in January 2024 to ₹27.98 in June 2025.

This is not audited profit. It subtracts estimated electricity costs and station rent/maintenance from recorded completed-swap revenue, but excludes battery depreciation, battery procurement, corporate overhead, customer acquisition, and other costs.

A separate revenue validation found material monthly differences between recorded charges and list price - discount beginning in October 2024. These differences reached approximately ₹557,611 in June 2025 and require an accounting/billing audit.
Business Recommendations
1. Audit tariff and billing discrepancies: Review PEAK, OFFPEAK, and PARTNER tariff rules, discounts, and billing adjustments.
2. Improve battery availability: Introduce minimum-inventory alerts and prioritize high-risk locations in Jaipur, Delhi NCR, and Hyderabad.
3. Inspect Launch-wave Gen1 stations: Review high-failure stations and prioritize upgrades based on evidence. Charger generation is confounded with expansion wave, station age, and site mix; the analysis cannot isolate a hardware-only effect.
4. Plan for evening peaks: Strengthen charging buffers and redistribution before 7 PM–10 PM.
5. Investigate 3W retention: Study rider needs, slot availability, pack turnaround, and plan structure before testing targeted interventions.
6. Build complete profitability monitoring: Reconcile revenue and include battery depreciation, procurement, operating overhead, electricity, rent, and maintenance.
Visualizations
Add your actual exported chart PNG files to the assets/ folder and update the filenames below. Do not use illustrative or internet-sourced charts.

Suggested chart order:
1. assets/monthly_business_performance.png
2. assets/city_operational_reliability.png
3. assets/charger_generation_comparison.png
4. assets/battery_availability_vs_failures.png
5. assets/hourly_no_battery_failures.png
6. assets/station_failure_priorities.png
7. assets/rider_cohort_retention.png
8. assets/contribution_proxy_and_revenue_variance.png
9. assets/python_dashboard.png (optional static dashboard preview)
Example Markdown image:
![Monthly business performance](assets/monthly_business_performance.png)
Repository Structure
volt-relay-energy-analytics/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── Data_analytics_hackathon.ipynb
├── assets/
│   ├── monthly_business_performance.png
│   ├── city_wise_perfomance.png
│   ├── battery_availability_vs_failures.png
How to Reproduce
1. Open the Google Colab notebook linked above.
2. Obtain access to the synthetic input datasets from the authorized project folder.
3. Update the notebook's data-folder path to match your Colab environment.
4. Install dependencies if needed:
pip install -r requirements.txt
5. Run the notebook cells in order to reproduce data preparation, analysis, visualizations, and dashboard exports.
The notebook may require the original dataset files and Google Drive access. Those files are not included in this repository by default.
Limitations
- The data is synthetic and covers only six cities over January 2024–June 2025.
- The analysis is observational; associations do not prove causation.
- Hourly minimum battery counts are not exact swap-time inventory.
- Battery commissioning-date inconsistencies prevent reliable battery-age analysis.
- Charger generation is confounded with expansion wave and station mix.
- The contribution proxy is incomplete and is not actual net profit.
- Revenue discrepancies from October 2024 onward remain unresolved.
- Cohort retention comparisons use complete 2024 cohorts; some segment sample sizes are small.
AI Usage Disclosure
AI assistance was used for selected coding support, debugging, analytical communication, and report structuring. Dataset inspections, DuckDB/Python analytical validations, empirical interpretations, and final editorial decisions were reviewed and verified as part of the project workflow.
Author
Fatima Jaffar
Individual Data Analytics Hackathon Submission
