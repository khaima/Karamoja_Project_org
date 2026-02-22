# Food Security & Crop Yield Analysis – Karamoja Region (2017)

![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

This project analyzes crop yield, production, and population data for the Karamoja region of Uganda to evaluate productivity differences between sorghum and maize, assess food availability per person, identify food security risk patterns, and test the statistical significance of yield differences.

---

## Project Overview

Karamoja is one of the most food insecure regions of Uganda. Low crop productivity, driven by drought, pests, and disease outbreaks, contributes significantly to food shortages. NGOs operating in the region lack comprehensive visibility into crop performance and food security conditions. This analysis uses modeled satellite‑based yield estimates to identify vulnerable areas and inform targeted interventions. The primary datasets contain subcounty‑ and district‑level agricultural production data, including crop yields, production totals, population, and derived food security indicators.

---

## Business Problem

**Stakeholders** (e.g., NGOs, government agencies, agricultural cooperatives) need to:

- Understand the key drivers of crop yield variability and food insecurity.
- Identify subcounties most at risk of food shortages.
- Compare the performance of sorghum vs. maize to guide crop selection and resource allocation.
- Quantify the relationship between population and total food production.
- Obtain actionable insights to design effective interventions and monitor their impact.

Without a data‑driven approach, decisions may rely on incomplete information, leading to inefficient resource distribution and missed opportunities to improve food security.

---

## Data Analysis Focus

The analysis focuses on:

1. **Data cleaning and preparation**: Handling missing values, removing duplicates, and treating outliers using the IQR method.
2. **Feature engineering**: Creating new variables to better measure food security dynamics:
   - `Total_Production` – combined sorghum and maize production.
   - `Food_per_Person` – total production divided by population, approximating food availability pressure.
   - `Yield_Gap` – difference between sorghum and maize yields.
   - `Risk_Level` – binary classification of subcounties as “High Risk” or “Lower Risk” based on median food availability.
3. **Exploratory data analysis**: Visualizing distributions, comparing yields, and exploring relationships between production and population.
4. **Statistical testing**: Performing a paired t‑test to determine whether sorghum and maize yields differ significantly.
5. **Export**: Saving the enriched dataset for further visualization in Tableau.

---

## Business Value

By delivering these analyses, the project enables:

- **Evidence‑based planning**: Interventions can be targeted to subcounties with the highest food risk.
- **Crop selection guidance**: Quantifying the yield advantage of maize over sorghum helps farmers and extension services choose appropriate crops.
- **Resource optimization**: Budgets and supplies can be allocated where food availability is lowest.
- **Impact assessment**: Baseline metrics (e.g., food per person) allow measurement of future program effectiveness.

Ultimately, this leads to improved livelihoods, reduced food insecurity, and more resilient communities in Karamoja.

---

## Data Sources

The analysis uses two CSV files containing 2017 agricultural and population data for Karamoja:

| File | Description |
|------|-------------|
| `Uganda_Karamoja_Subcounty_Crop_Yield_Population.csv` | Subcounty‑level data including crop yields (sorghum and maize), production totals, population, and area. |
| `Uganda_Karamoja_District_Crop_Yield_Population.csv` | District‑level aggregated data (used for comparison but not the focus of the final export). |

The datasets contain modeled satellite‑based yield estimates. All data are included in the repository (or can be obtained from the provided sources).

---

## Data Preparation

The data preparation steps are performed in the Jupyter notebook `karamoja.ipynb` and include:

1. **Loading data**: Reading the two CSV files into pandas DataFrames.
2. **Initial inspection**: Checking column names, data types, missing values, and basic statistics.
3. **Handling missing values**:
   - Dropping rows with any missing values (the dataset is complete, so this has no effect).
   - For completeness, numeric missing values are filled with the median (though not required here).
4. **Removing duplicates**: Ensuring no duplicate records exist.
5. **Outlier treatment**:
   - Visualizing yield and production distributions with boxplots.
   - Capping outliers using the interquartile range (IQR) method for key numeric columns (`S_Yield_Ha`, `M_Yield_Ha`, `S_Prod_Tot`, `M_Prod_Tot`, `Total_Production`, `Food_per_Person`).
6. **Feature engineering**:
   - `Total_Production = S_Prod_Tot + M_Prod_Tot`
   - `Food_per_Person = Total_Production / POP`
   - `Yield_Gap = S_Yield_Ha - M_Yield_Ha`
   - `Risk_Level = "High Risk" if Food_per_Person < median else "Lower Risk"`
7. **Export**: Saving the cleaned and enriched subcounty dataset as `karamoja_clean.csv` for use in Tableau or further analysis.

---

## Data Understanding

Exploratory analysis reveals:

- **Yield distributions**:
  - Maize yields are substantially higher on average (~941 kg/ha) than sorghum yields (~274 kg/ha).
  - Both crops exhibit a wide range of yields across subcounties, indicating variability in growing conditions or farming practices.
- **Food availability**:
  - `Food_per_Person` varies widely (from near zero to over 200 kg/person). The median is used to classify risk.
  - A histogram shows a right‑skewed distribution, with many subcounties having relatively low food availability.
- **Risk classification**:
  - Subcounties classified as “High Risk” have significantly lower food per person, as visualized in a boxplot.
- **Production vs. population**:
  - A scatter plot shows a weak positive relationship; some high‑population areas have low production, indicating potential food deficits.
- **Yield comparison**:
  - A paired boxplot confirms that maize yields are consistently higher than sorghum yields across subcounties.
  - The mean yield gap (sorghum – maize) is strongly negative (~ -667 kg/ha).

---

## Key Insights

1. **Maize outperforms sorghum**: Maize yields are, on average, more than three times higher than sorghum yields. The difference is statistically significant (paired t‑test, p‑value ≈ 3.6e-24).
2. **Wide variability in food availability**: Food per person ranges from 0.006 to 216 kg, highlighting extreme disparities. The median is about 37 kg/person.
3. **Risk hotspots**: 26 subcounties (half the dataset) fall below the median food availability and are classified as “High Risk”. These areas should be prioritized for interventions.
4. **Population pressure**: Some densely populated subcounties have low total production, suggesting they may rely on food imports or face chronic shortages.
5. **Outliers**: Several subcounties have exceptionally high production or yields; these could serve as benchmarks or best‑practice examples.

---

## Business Impact

The insights from this analysis have already informed several decisions:

- **Targeted interventions**: NGOs and local government can use the risk classification to direct food aid, seed distributions, and agricultural training to the most vulnerable subcounties.
- **Crop promotion**: The clear yield advantage of maize supports efforts to encourage maize cultivation where conditions are suitable, while also recognizing that sorghum may be preferred for drought tolerance in some areas.
- **Baseline for monitoring**: The exported dataset (`karamoja_clean.csv`) provides a baseline against which future interventions can be measured.

---

## Recommendations

Based on the analysis, we recommend:

1. **Promote maize cultivation** in areas with adequate rainfall or irrigation to boost overall food production.
2. **Target high‑risk subcounties** with a combination of short‑term food assistance and long‑term agricultural support (improved seeds, extension services, soil management).
3. **Investigate drivers of yield variability** – collect additional data on farming practices, input use, and environmental factors to understand why yields differ so widely.
4. **Establish a monitoring system** using the `Food_per_Person` metric to track changes over time and evaluate the impact of interventions.
5. **Conduct a deeper analysis** of the relationship between population and production to identify subcounties where population growth may outstrip local food production capacity.

---

## Getting Started

### Prerequisites
- Python 3.8+
- Required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`

Install dependencies with:
```bash
pip install -r requirements.txt
