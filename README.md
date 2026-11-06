# 📱 Google Play Growth Intelligence

![Python](https://img.shields.io/badge/Python-3.11+-blue?style=for-the-badge&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-black?style=for-the-badge&logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Scientific_Computing-blue?style=for-the-badge&logo=numpy)
![SciPy](https://img.shields.io/badge/SciPy-Statistical_Analysis-8CAAE6?style=for-the-badge&logo=scipy)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Preprocessing-orange?style=for-the-badge&logo=scikitlearn)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange?style=for-the-badge&logo=matplotlib)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical_Plots-green?style=for-the-badge)
### A Product & Market Analytics Case Study

An end-to-end product analytics project exploring the Google Play Store ecosystem through data quality assessment, exploratory analysis, statistical testing, and a scenario-based market opportunity framework.

> **Project objective:** Understand how app category, user feedback, pricing, app size, content rating, and update recency relate to app adoption—and identify categories that appear attractive under different demand-versus-competition assumptions.

---

## Table of Contents

1. [Business Context](#1-business-context)
2. [Key Questions](#2-key-questions)
3. [Dataset](#3-dataset)
4. [Tools & Libraries](#4-tools--libraries)
5. [Workflow](#5-workflow)
6. [Analysis & Methods](#6-analysis--methods)
7. [Key Findings](#7-key-findings)
8. [Market Opportunity Framework](#8-market-opportunity-framework)
9. [Business Implications](#9-business-implications)
10. [How to Run](#10-how-to-run)
11. [Repository Structure](#11-repository-structure)
12. [Limitations](#12-limitations)
13. [Possible Extensions](#13-possible-extensions)

---

## 1. Business Context

A large app marketplace contains applications with very different levels of visibility, adoption, ratings, and commercial performance. Aggregate download volume alone does not explain whether a category is saturated, whether a typical app performs well, or whether users respond differently to paid apps and recently updated apps.

This case study uses a historical Google Play Store dataset to examine marketplace patterns and build a transparent, exploratory framework for comparing app categories. The analysis is descriptive and associational; it does not establish that any app attribute causes higher installs or ratings.

## 2. Key Questions

- How is the app marketplace distributed across categories and genres?
- How complete, valid, and consistent is the source data?
- How do ratings, reviews, installs, pricing, and app size vary across categories?
- Do paid and free apps show different adoption and rating patterns?
- Which content-rating groups account for the greatest install volume?
- Are app size and review volume associated with installs?
- Do apps with different update recency show different ratings or install levels?
- Which categories remain attractive when the relative importance of demand and competition changes?

## 3. Dataset

The project uses a Google Play Store app dataset containing app-level attributes such as:

| Field | Description |
|---|---|
| `App` | Application name |
| `Category` | Main Play Store category |
| `Rating` | User rating |
| `Reviews` | Number of reviews |
| `Size` | App size as represented in the source |
| `Installs` | Install-count bucket/value |
| `Type` | Free or paid |
| `Price` | Listed app price |
| `Content Rating` | Intended audience classification |
| `Genres` | App genre classification |
| `Last Updated` | Most recent update date in the dataset |
| `Current Ver` | Current app version |
| `Android Ver` | Minimum Android version information |

The notebook's cardinality analysis reports **9,659 unique app names, 119 genres, and 33 categories**. The missing-value audit reports **1,474 missing ratings (13.60%)**; missingness in several other fields is much smaller.

The dataset is a historical snapshot, not a live feed of the current Google Play Store. Refer to the source dataset and notebook for its exact provenance and any additional preprocessing details.

## 4. Tools & Libraries

- **Python** — analysis and data preparation
- **Pandas, NumPy** — cleaning, transformation, aggregation, and feature engineering
- **Matplotlib, Seaborn** — visual exploration
- **SciPy** — statistical tests and correlation analysis
- **Statsmodels** — Tukey's HSD post-hoc comparisons
- **Scikit-learn** — feature scaling for the opportunity scoring framework
- **Jupyter Notebook** — reproducible analysis environment

## 5. Workflow

1. **Understand the data** — inspect dimensions, columns, data types, and category structure.
2. **Audit data quality** — assess missingness, duplicates, invalid values, inconsistent formats, and business-rule violations.
3. **Prepare the data** — clean malformed values, correct data types, and derive analysis-ready fields.
4. **Explore the marketplace** — compare app counts, installs, ratings, reviews, pricing, and other app attributes.
5. **Test relationships** — use rank-based correlation and group-comparison tests where appropriate.
6. **Compare categories** — examine demand, typical app adoption, competition, and paid-app presence.
7. **Run sensitivity analysis** — recalculate opportunity rankings under multiple demand/competition weightings.
8. **Translate findings** — state practical implications while documenting uncertainty and limitations.

## 6. Analysis & Methods

### Data Quality and Preparation

The notebook audits missing values and data types, checks duplicate records and invalid values, and validates business rules. For example, it identifies an impossible rating above the valid 1–5 range and removes that invalid record. It also identifies a row with a missing app type that is removed because the value cannot be reliably inferred.

The missing-rating rate is material (13.60%). Rating-based analysis should therefore distinguish observed ratings from any imputed values. The notebook creates a missing-rating indicator for this purpose; statistical comparisons of ratings should be based on observed ratings rather than treating imputed values as genuine user feedback.

### Exploratory Data Analysis

The notebook explores:

- Marketplace composition and category competition
- Rating distributions and category-level satisfaction
- Total and median installs by category
- Free-versus-paid app patterns
- Content-rating groups and install volume
- App size versus installs
- Review volume versus installs
- Update recency versus ratings and installs

### Statistical Analysis

| Method | Purpose |
|---|---|
| Spearman rank correlation | Assess monotonic association without requiring a linear relationship or normally distributed variables |
| One-way ANOVA | Test whether mean outcomes differ across multiple update-recency groups |
| Tukey's HSD | Identify which pairs of groups differ after an ANOVA result |

The notebook reports a Spearman correlation of approximately **0.342** between app size and log-transformed installs. This is a statistically significant but comparatively modest positive association; it should not be interpreted as evidence that larger app size causes more downloads.

For update recency, the notebook reports:

- **Rating ANOVA:** F ≈ 63.24, p ≈ 8.48 × 10⁻⁵³.
- **Log-installs ANOVA:** F ≈ 331.23, p ≈ 1.12 × 10⁻²⁶⁸.

These tests indicate that at least one update-recency group mean differs for each outcome. Tukey's HSD is then used to examine pairwise differences in log-installs. Statistical significance does not establish causality, and ANOVA conclusions depend on assumptions such as independent observations and appropriate variance behavior.

## 7. Key Findings

The following are descriptive findings from the notebook's current analysis and should be interpreted within the dataset's historical scope.

- **Marketplace demand is unevenly distributed.** The GAME category has the largest total recorded install volume in the notebook's category comparison.
- **High total installs and strong typical-app performance are not identical.** COMMUNICATION shows substantial total demand across fewer apps, while PHOTOGRAPHY has a comparatively high median install count.
- **Ratings are concentrated toward the higher end.** Category-level averages vary; the notebook highlights Events and Education among categories with comparatively high average ratings.
- **Free apps dominate broad adoption.** Paid-app patterns differ by category; the notebook flags Weather as interesting for paid-app adoption and GAME as having the largest paid-app ecosystem.
- **Audience size matters when interpreting install totals.** Everyone-rated apps account for the largest total install volume, while some smaller content-rating groups have higher median installs. Small groups require caution.
- **App size is not a strong standalone explanation of adoption.** Its association with log-installs is positive but modest, and category may confound the relationship.
- **Reviews are associated with adoption.** Apps with more reviews generally tend to have more installs, but review volume is not a complete explanation of install behavior.
- **Update recency is associated with both ratings and install levels.** Recently updated groups show higher average values in the notebook's summary, but the available `Last Updated` field measures recency—not update frequency or maintenance quality.

## 8. Market Opportunity Framework

The final section creates a simple category-level score using two dimensions:

- **Demand:** median installs for apps in a category.
- **Competition:** number of apps in that category.

Categories with fewer than 10 apps are excluded from this scoring exercise to reduce the influence of very small groups. Demand and app count are min-max scaled. The competition dimension is inverted so that fewer competing apps produce a higher low-competition score.

The notebook compares three weighting scenarios:

| Scenario | Demand Weight | Low-Competition Weight |
|---|---:|---:|
| Demand-focused | 70% | 30% |
| Balanced | 50% | 50% |
| Competition-focused | 30% | 70% |

For each category, the notebook calculates a score and rank under each scenario, then compares average rank and rank range. This makes it possible to distinguish categories that remain highly ranked across assumptions from categories whose attractiveness depends heavily on the chosen weights.

### Opportunity Signals

- **Entertainment, Photography, Weather, and Education** appear among the strongest categories across the three scenarios, with comparatively stable rankings.
- **House & Home, Food & Drink, and Comics** show relatively low competition, but their overall attractiveness is more sensitive to the weighting scenario. They may be niche opportunities rather than obvious top priorities.

This is a heuristic prioritization model—not a validated market-size, revenue, profitability, or unmet-demand estimate. A low app count does not automatically mean a category is underserved.

## 9. Business Implications

- Evaluate categories using both total demand and median app-level adoption; either metric alone can create a misleading picture.
- Treat categories with stable rankings across scenarios as stronger candidates for deeper research, not as automatic investment decisions.
- Investigate paid-app adoption separately by category rather than assuming one monetization strategy works across the marketplace.
- Consider review volume as one useful popularity signal, while recognizing that it may reflect app age, visibility, and category scale.
- Treat update recency as a descriptive signal. The dataset does not show the number or cadence of updates, so it cannot support conclusions about update frequency.
- Before acting on a category opportunity, validate it with current market data, competitor quality, revenue estimates, user needs, acquisition costs, and qualitative research.

## 10. How to Run

1. Clone or download this repository.
2. Place the dataset file in the path expected by the notebook, or update the notebook's data-loading cell to point to your local file.
3. Install the required packages:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn jupyter
```

4. Launch Jupyter:

```bash
jupyter notebook
```

5. Open `Google_Play_Growth_Intelligence_A_Product_Analytics_Case_Study.ipynb` and run the notebook from top to bottom.

> **Reproducibility note:** The dataset is not embedded in this README. Add the dataset file to the repository only if its license and redistribution terms permit it. Update the notebook's file path to match your repository structure.

## 11. Repository Structure

A clean repository can follow this structure:

```text
Google-Play-Growth-Intelligence/
│
├── data/
│   └── google_play_store.csv
│
├── notebooks/
│   └── Google_Play_Growth_Intelligence_A_Product_Analytics_Case_Study.ipynb
│
├── images/
│   └──
│
├── README.md
└── requirements.txt
```

## 12. Limitations

- **Historical snapshot:** Results describe the supplied dataset and should not be presented as current Play Store market conditions.
- **Approximate installs:** Install values are represented by buckets/rounded counts in the source, so derived totals and comparisons are approximate.
- **Missing ratings:** A meaningful share of apps has no rating. Imputation can affect descriptive summaries; rating-based inference should use observed ratings and report the sample size.
- **Observational data:** Correlation and group differences do not establish cause and effect.
- **Potential confounding:** Category, app age, brand recognition, marketing, and other omitted variables may influence installs and ratings.
- **Update recency is not update frequency:** Only the most recent update date is available.
- **Heuristic opportunity score:** Median installs and app count are proxies. The score does not measure market size, revenue, profitability, competition quality, or consumer demand directly.
- **Statistical assumptions:** ANOVA and post-hoc results should be accompanied by checks for independence and variance assumptions; use alternatives such as Welch's ANOVA when appropriate.

## 13. Possible Extensions

- Add confidence intervals and group sample sizes to category comparisons.
- Check ANOVA assumptions and compare results with Welch's ANOVA and suitable post-hoc procedures where needed.
- Use robust or bootstrap-based estimates for skewed install distributions.
- Add revenue or monetization data to distinguish adoption from commercial performance.
- Incorporate current market data and competitor-level quality indicators.
- Improve the opportunity score with more dimensions, transparent business weights, and validation against external outcomes.
- Build an interactive dashboard in Power BI or Streamlit for category and scenario exploration.

---

## Author

**Kashish Pundir**  
B.Tech, Computer Science & Engineering (Data Science)

*This project is an independent product and market analytics case study built for portfolio and learning purposes.*
