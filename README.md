Project Overview
Karamoja is one of the most food-insecure regions of Uganda. Low crop productivity—driven by drought, pests, and disease—contributes to chronic food shortages. NGOs and government agencies lack comprehensive visibility into crop performance and food security conditions. This analysis uses modeled satellite‑based yield estimates to identify vulnerable areas, quantify the yield gap between sorghum and maize, and provide actionable insights for targeted interventions.

Business Problem
Stakeholders (NGOs, government, agricultural cooperatives) need to:

Understand key drivers of yield variability and food insecurity.

Identify subcounties most at risk of food shortages.

Compare sorghum vs. maize performance to guide crop selection and resource allocation.

Quantify the relationship between population and food production.

Obtain evidence‑based insights to design effective interventions and monitor impact.

Without a data‑driven approach, decisions risk being inefficient, missing opportunities to improve food security.

Data Analysis Focus
The analysis centers on:

Data cleaning & preparation: Handling missing values, removing duplicates, and capping outliers using the IQR method.

Feature engineering: Creating new metrics—Total_Production (sorghum + maize), Food_per_Person, Yield_Gap (sorghum – maize), and Risk_Level (binary classification based on median food availability).

Exploratory analysis: Visualizing distributions, comparing yields, and exploring production‑population relationships.

Statistical testing: Paired t‑test to determine if sorghum and maize yields differ significantly.

Export: Saving the enriched dataset (karamoja_clean.csv) for Tableau visualization.

Business Value
This project enables:

Evidence‑based planning: Interventions can be targeted to the highest‑risk subcounties.

Crop selection guidance: Quantifying maize’s yield advantage helps farmers and extension services choose appropriate crops.

Resource optimization: Budgets and supplies can be allocated where food availability is lowest.

Impact assessment: Baseline metrics (e.g., food per person) allow measurement of program effectiveness.

Ultimately, it supports improved livelihoods and more resilient communities in Karamoja.

Data Sources
Two CSV files (2017) are used:

Subcounty‑level data: Includes yields (sorghum, maize), production totals, population, and area.

District‑level data: Aggregated for comparison (not the focus of the final export).

Data are modeled satellite‑based yield estimates; all files are included in the repository.

Data Preparation
Steps performed in karamoja.ipynb:

Load data into pandas DataFrames.

Inspect column names, types, missing values, and basic statistics.

Handle missing values (dataset complete; median fill used as safeguard).

Remove duplicates.

Treat outliers via IQR capping for key numeric columns.

Engineer features:

Total_Production = S_Prod_Tot + M_Prod_Tot

Food_per_Person = Total_Production / POP

Yield_Gap = S_Yield_Ha - M_Yield_Ha

Risk_Level = "High Risk" if Food_per_Person < median else "Lower Risk"

Export cleaned dataset to karamoja_clean.csv.

Data Understanding
Yield distributions: Maize yields (~941 kg/ha) are substantially higher on average than sorghum (~274 kg/ha), with wide variability across subcounties.

Food availability: Food_per_Person ranges from near 0 to >200 kg/person; distribution is right‑skewed, with many subcounties below the median.

Risk classification: “High Risk” subcounties have significantly lower food per person (boxplot confirms).

Production vs. population: Weak positive relationship; some densely populated areas have low production, indicating potential deficits.

Yield gap: Mean gap (sorghum – maize) is strongly negative (~ -667 kg/ha); paired boxplot shows maize consistently outperforms sorghum.

Key Insights
Maize outperforms sorghum: Maize yields >3× higher than sorghum; difference is statistically significant (paired t‑test, p‑value ≈ 3.6e‑24).

Wide food availability disparity: Food per person ranges 0.006–216 kg; median ≈37 kg/person.

Risk hotspots: 26 subcounties (half the dataset) are “High Risk” and should be prioritized.

Population pressure: Some high‑population subcounties have low total production, suggesting reliance on external food sources.

Outliers: A few subcounties with exceptionally high yields/production can serve as benchmarks.

Business Impact
Targeted interventions: NGOs and government can direct aid, seeds, and training to the most vulnerable subcounties.

Crop promotion: Clear evidence supports promoting maize where conditions allow, while recognizing sorghum’s drought tolerance in marginal areas.

Baseline for monitoring: Exported dataset enables future impact measurement.

Recommendations
Promote maize cultivation in areas with adequate rainfall/irrigation to boost food production.

Target high‑risk subcounties with combined short‑term assistance and long‑term agricultural support.

Investigate yield variability drivers – collect additional data on farming practices, inputs, and environmental factors.

Establish a monitoring system using Food_per_Person to track changes and evaluate interventions.

Conduct deeper analysis of production‑population dynamics to anticipate future deficits.
