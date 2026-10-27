# Bayesian modelling of penguin body mass

An individual RMIT University analytics course project examining how penguin body mass is associated with flipper length, species and recorded sex. The analysis uses Bayesian regression to compare explanations and communicate uncertainty in both coefficients and individual predictions.

**Key finding:** accounting for sex substantially changes the estimated flipper–mass association. Evidence for additional species-specific slopes is weak and sensitive to prior assumptions, so the report retains uncertainty rather than declaring one complex model a clear winner.

## Project at a glance

| Area | Details |
| --- | --- |
| Context | Applied Bayesian Statistics coursework, October 2026 |
| Tools | R, JAGS, `rjags`, `coda` |
| Data | Public Palmer Penguins data; 344 starting records |
| Analysis samples | 342 baseline records; 333 common records for all candidate-model comparisons |
| Methods | Bayesian linear regression, MCMC diagnostics, prior sensitivity, Bayes factors and model averaging |
| Repository contents | This summary and a [detailed project overview](project_overview.md) |

## What the analysis demonstrates

- **Data preparation:** define missing-value rules and use identical rows when comparing models.
- **Statistical modelling:** compare a species-adjusted model, a sex-adjusted extension and a model with species-specific flipper slopes.
- **Validation:** assess chain behaviour, effective sample size and numerical consistency; distinguish computational checks from assumptions about the data.
- **Communication:** explain adjusted associations, sensitivity to modelling choices and the difference between mean-response and individual predictive uncertainty.

## Selected findings

- On the same 333 records, the expected body-mass difference associated with 10 mm longer flippers changes from approximately **399 g** to **205 g** after sex adjustment.
- Under the sex-adjusted common-slope model, the estimated male–female difference is approximately **525 g**, conditional on species and flipper length.
- With equal model priors, the species-specific-slope model receives approximately **55%** posterior weight. Doubling coefficient-prior standard deviations reduces that weight to approximately **21%**, showing uncertainty about the added complexity.

These are observational associations under the stated models. Reported fit measures are **in-sample**; this project does not establish performance on held-out data.

## How to explore

Read the [project overview](project_overview.md) for sample definitions, model choices, diagnostics, detailed results and limitations. The public data are available from the [Palmer Penguins project](https://allisonhorst.github.io/palmerpenguins/), which credits Kristen Gorman and Palmer Station LTER.

## Provenance and AI assistance

This portfolio summarises the completed coursework report and quotes results from its recorded R/JAGS execution on 22 October 2026. No new model execution was performed during portfolio preparation. Source scripts, saved chains and the execution archive are not included here, so the repository currently serves as a documented case study.

The original report acknowledges ChatGPT assistance with source checking, R/JAGS and report-generation code, diagnostic checks and explanatory drafting. This portfolio preserves that disclosure. It does not claim that all coding or writing was completed without AI assistance.
