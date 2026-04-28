# 🛒 Does Where You Live Determine What You Eat?
### Tesco Grocery Data Analysis — London Neighbourhood Diet & Income Study

> Mapping how neighbourhood income shapes diet quality across 4.5 million Londoners, from protein consumption to drink choices, using actual grocery purchase data.

---

## 📋 Project Overview

This project analyses the **Tesco Grocery 1.0 Dataset** (Aiello et al., 2020 — *Scientific Data*) to investigate the relationship between neighbourhood income, age, and dietary quality across Greater London. Using anonymised Clubcard purchase records from 2015, we explore two core research questions:

1. **Does income predict dietary quality?** (protein intake, health scores)
2. **Does neighbourhood age shape drink choices?** (wine vs. soft drinks vs. beer)

### Key Findings

| Finding | Result |
|--------|--------|
| Protein ↔ Borough Health Score | r = **0.942** (p < 0.001) — strongest single finding |
| Income → Wine (via Age) | ~**34%** of income–wine gradient runs through age pathway |
| Protein range (poorest → richest) | 10.75% (Newham) → 12.89% (Kensington & Chelsea) |
| NHS protein target (20% of calories) | ❌ **No London borough reaches this** |

---

## 📁 Repository Structure

```
.
├── Tesco_Data.ipynb                  # Main analysis notebook (Google Colab)
├── ADS_Infographics_Final.pdf        # Infographic poster summarising findings
├── presentation/
│   └── Marketing_Strategy_Proposal.pptx   # Full presentation with references
└── README.md
```

---

## 📊 Dataset

**Source:** [Tesco Grocery 1.0](https://www.nature.com/articles/s41597-020-0397-7) — Aiello et al., *Scientific Data*, 2020

**Supplementary income data:**
- [HMRC Income Data](https://www.gov.uk/government/statistics/personal-incomes-statistics) — borough-level earnings
- [ONS Household Income](https://www.ons.gov.uk/) — modelled neighbourhood estimates

### Geographic Coverage

| Level | Units | Description |
|-------|-------|-------------|
| Borough | 33 | All London Boroughs |
| MSOA | 983 | Medium Super Output Areas |
| LSOA | 4,833 | Lower Super Output Areas |
| Ward | 638 | Electoral Wards |

### Data Schema (Key Field Groups)

| Group | Columns | Description |
|-------|---------|-------------|
| Geographic & Coverage | `area_id`, `representativeness_norm` | Area identifiers; filter on `representativeness_norm > 0.10` |
| Basket Fractions | `f_fruit_veg`, `f_wine`, `f_sweets`, `f_protein_*`, … | Spend share per food category (sum ≈ 1.0) |
| Nutrient Distributions | `protein_perc50`, `sugar_perc75`, … | Percentile distributions of nutrient content |
| Health Index | `h_nutrients_calories_norm` | Composite diet quality score (higher = healthier) |
| Demographics | `avg_age`, `people_per_sq_km` | Area-level demographic context |

---

## ⚙️ Setup & Usage

### Requirements

- Python 3.8+
- Google Colab (recommended) or local Jupyter environment

### Dependencies

```bash
pip install pandas numpy scipy matplotlib seaborn statsmodels
```

### Running the Notebook

1. Mount your Google Drive in Colab:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. Set your data folder path in the notebook:
   ```python
   folder_path = 'your/drive/path/to/data'
   ```

3. The notebook will load all 48 DataFrames (12 months × 4 geographic levels) automatically.

### Data File Naming Convention

```
year_borough_grocery.csv        ← Annual borough-level
Jan_msoa_grocery.csv            ← Monthly MSOA-level
Feb_lsoa_grocery.csv            ← Monthly LSOA-level
```

---

## 🔍 Analysis Summary

### Insight 1 — Age & Drink Composition

Drink basket share shifts systematically with neighbourhood average age:
- **Wine** rises ~35% from youngest to oldest areas (r = +0.31, p < 0.001)
- **Soft drinks** fall in near-perfect symmetry (r = −0.23)
- **Beer** remains age-neutral (not significant)

**Mediation Analysis (Baron–Kenny):** ~34% of the income–wine gradient is mediated through age (bootstrap indirect effect = +0.13, 95% CI excludes zero). Income retains a significant direct effect (c′ = +0.34, p < 0.001).

### Insight 2 — Income & Protein Intake

Protein energy share is the strongest geographic marker of dietary quality in London:

- Richest 20% of boroughs: **12.5%** calories from protein
- Poorest 20%: **11.5%** calories from protein
- Borough health score correlation: **r = 0.942** (p < 0.001, n = 33)
- All 33 boroughs fall below the NHS recommended 20% protein target

---

## ⚠️ Limitations

| Limitation | Impact |
|-----------|--------|
| **Clubcard sampling (~44% of shoppers)** | Under-represents lower-income and elderly shoppers |
| **Single retailer** | Excludes Waitrose/M&S (affluent) and Lidl/Aldi (budget); likely compresses true income gradient |
| **Ecological fallacy** | All data are area-level; individual-level inferences are not valid |
| **2015 snapshot** | Pre-COVID; purchasing patterns may have shifted significantly |
| **No price data** | Spend fractions cannot separate quantity changes from price changes |
| **LSOA variance 6× higher than borough** | Borough statistics mask extreme local inequality |

---

## 👥 Team

<!-- Add your team members below -->
| Name | Role |
|------|------|
|  |  |
|  |  |
|  |  |

---

## 📄 References

Full references are available in the accompanying presentation. Key sources:

1. Aiello et al. (2020). Tesco Grocery 1.0. *Scientific Data.*
2. Baron & Kenny (1986). Mediation analysis framework.
3. HMRC Personal Income Statistics.
4. ONS Household Income Estimates for Small Areas.
5. NHS Dietary Guidelines — protein recommendations.

---

## 📜 License

This project uses publicly available academic data. Please cite the original Tesco Grocery 1.0 dataset (Aiello et al., 2020) if you build upon this work.
