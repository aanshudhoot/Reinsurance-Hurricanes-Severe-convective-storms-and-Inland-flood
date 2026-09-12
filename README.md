# Property Catastrophe Reinsurance Program: Pricing & Design (NOAA Case Study)

USD 1B portfolio analysis using 50+ years of public NOAA Storm Events data to design and price a property catastrophe reinsurance program for a hypothetical U.S. regional insurer.

## Overview

This project simulates the work of a reinsurance pricing analyst: building a catastrophe reinsurance program for a regional insurer with USD 1,000M in aggregate property exposure across the United States, covering three peril types — hurricanes/tropical storms, severe convective storms (tornadoes, thunderstorms), and inland flooding.

The analysis combines traditional actuarial techniques (frequency-severity modeling, extreme value theory) with modern data science approaches (machine learning for severity segmentation, SHAP interpretability) to price multiple reinsurance structures and stress-test them under adverse scenarios.

## Data

- **NOAA NCEI Storm Events Database** — [https://www.ncei.noaa.gov/stormevents/](https://www.ncei.noaa.gov/stormevents/)
- **Synthetic exposure data** — a 1,000-policy sample (`synthetic_exposure_US_1bn_policies_1000_sample.csv`, random seed = 42) representing the USD 1B portfolio

## Methodology

1. **Data preparation & EDA** — Cleaned NOAA event-level data and scaled economic losses to estimated insured losses using documented assumptions. Explored frequency trends over time and severity distributions.

2. **Frequency & severity modeling** — Fit a Poisson/Negative Binomial frequency model (with over-dispersion diagnostics) and a severity model combining a Lognormal/Gamma body with a Peaks-Over-Threshold (POT–GPD) tail for extreme losses.

3. **Aggregate loss simulation** — Built a compound-sum Monte Carlo simulator to generate simulated annual aggregate losses and per-event loss distributions across thousands of simulated years.

4. **Treaty pricing** — Priced four reinsurance structures:
   - Quota-share (30%) with ceding commission
   - Per-occurrence excess-of-loss, layered (e.g., USD 10M retention; Layer A: 10M–50M; Layer B: 50M–150M)
   - Aggregate excess-of-loss (stop-loss)
   - Multi-year layered program with reinstatement provisions

5. **Reinstatements & spatial correlation** — Modeled a single automatic (pro-rata) reinstatement and tested two approaches to spatial dependence between events: footprint-based scaling and a Gaussian-copula method.

6. **ML severity segmentation** — Trained an XGBoost model to predict event severity from location and magnitude features, with SHAP/permutation importance to interpret key loss drivers, benchmarked against the parametric approach.

7. **Sensitivity & stress testing** — Evaluated impacts of frequency uplift (+10%, +25%), fatter-tailed severity, and a hardening market (+20% rates) on premium and retained risk.

8. **Recommendation** — Compared 2–3 candidate reinsurance programs on expected premium, retained volatility, and trade-offs, with negotiation levers for placement.


## Key Outputs

- Frequency and severity model fits with diagnostic plots
- Simulated aggregate loss distribution for the USD 1B portfolio
- Priced reinsurance layers (expected loss, probability of exhaustion, premium)
- Sensitivity analysis under stress scenarios
- Recommended reinsurance program options

