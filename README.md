# Texas Bridge Condition — Regression Analysis

**MSc Data Science & AI coursework — 80%**

## Brief

The Texas Department of Transportation wanted to know which factors most influence the condition of their bridges, and how well those factors can predict it, using ~34,000 bridge records covering age, usage, material, and design. The catch: the report had to be written for a domain-expert stakeholder (a corrosion/materials specialist) who cares about the reasoning behind the analysis, not the code itself.

## Approach

- **Target construction**: derived a single 0–27 "current condition" score from three separate sub-ratings (deck, superstructure, substructure), and justified treating this ordinal score as continuous for regression given the number of score levels.
- **Category consolidation**: several material/design categories had very small sample sizes (e.g. Masonry, Suspension). Rather than dropping them outright, I compared their score distributions to larger categories and merged only where the underlying patterns were genuinely similar, preserving categories that showed distinct behaviour (e.g. Timber's consistently lower scores).
- **Outlier handling**: excluded bridges over 100 years old, reasoning through the maintenance/bias implications rather than dropping them by default.
- **Exploratory analysis**: correlation heatmap and cross-tabulations to check predictor relationships and collinearity risk; KDE plots comparing category age distributions to explain historical construction trends (e.g. a visible post-war steel boom, and a slowdown from the 1970s).
- **Modelling**: linear regression (scikit-learn) with standardised coefficients so predictor influence could be compared directly, plus residual analysis to check model fit.

## Results

- **R² = 0.45**, **RMSE = 2.11** (on a 27-point scale) — a moderate fit given only 5 candidate predictors.
- **Bridge age** was by far the strongest predictor (correlation −0.59 with condition), followed by **Steel** and **Timber** material types.
- **Average daily use** and **percentage truck traffic** had negligible effect — flagged early in the exploratory phase and confirmed by the final model.
- Residuals were roughly normal around zero but with a long tail, showing the model tends to over-predict condition for the worst bridges.

## What I'd do next

Drop the two negligible predictors to simplify the model, do a further pass on outliers, and test a higher-order polynomial fit — the age relationship may not be strictly linear.

## Stack

Python, pandas, scikit-learn, seaborn/matplotlib
