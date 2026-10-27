# Project overview

## Purpose and conclusion

This individual Applied Bayesian Statistics coursework project examines how flipper length, species and recorded sex relate to penguin body mass. It compares Bayesian regression models and reports how the results change when the adjustment variables or prior assumptions change.

The analysis supports a positive flipper–mass association, with a substantially smaller estimated association after sex adjustment. Including sex is strongly supported within the candidate models. Evidence for species-specific slopes is much weaker and sensitive to priors. Individual predictions remain considerably less precise than estimates of an average response.

## Data and sample preparation

The analysis uses the public Palmer Penguins dataset, with Adelie, Chinstrap and Gentoo observations collected across three Antarctic islands during 2007–2009. The data were collected and made available by Kristen Gorman and Palmer Station LTER; the curated package is maintained by Allison Horst, Alison Hill and Kristen Gorman. See the [official dataset documentation](https://allisonhorst.github.io/palmerpenguins/).

| Sample | Records | Inclusion rule | Purpose |
| --- | ---: | --- | --- |
| Starting curated data | 344 | All records | Establish the starting population of records |
| B342 baseline | 342 | Remove two records missing required body-mass or flipper measurements | Retain the presentation-baseline specification |
| M0, M1 and M2 comparison | 333 | Additionally remove nine records missing sex | Compare every candidate on identical observations |

No missing values were imputed, and no observation was excluded solely for being extreme. Fitting M0 again on the 333 comparison records prevents a sample change from being mistaken for an improvement due to sex adjustment. Complete-case selection may still be non-random.

The response is body mass in grams. Flipper length is centred at 200.9152047 mm. Adelie is the reference species and female is the reference sex. Island and year provide descriptive context; they are not fitted adjustment variables.

## Candidate models and priors

Each candidate assumes normally distributed conditional errors and a common residual variance.

| Model | Predictors | Analysis records |
| --- | --- | ---: |
| B342 | Centred flipper length and species | 342 |
| M0 | Same specification as B342, refitted on the comparison sample | 333 |
| M1 | M0 plus recorded sex | 333 |
| M2 | M1 plus flipper-length interactions with species | 333 |

M1 estimates one flipper slope after species and sex adjustment. M2 permits a different flipper slope for each species, while retaining a common sex contrast. These are conditional associations; changing an adjustment variable changes the question being answered.

The report uses proper regularising priors: a Normal(4000, 1000²) intercept prior, Normal(0, 20²) slope and slope-difference priors, Normal(0, 500²) species and sex contrast priors, and a Gamma precision prior with shape 2 and rate 250000. These were exploratory analyst choices, rather than preregistered or independently elicited biological beliefs.

Sensitivity checks double the coefficient-prior standard deviations, vary the precision-prior rate, and compare equal prior model probabilities with a preference for simpler models. The normal likelihood also gives a small prior-predictive probability to impossible negative masses; this is a disclosed modelling limitation.

## Computation and diagnostic checks

The coursework report records an R/JAGS execution completed on 22 October 2026, using R 4.4.2, JAGS 4.3.2, `rjags` 4-17 and `coda` 0.19-4.1. These are the reported execution versions, not a claim about the newest releases.

The reported workflow used four dispersed chains, adaptation separate from a 5,000-iteration burn-in, and at least 12,000 retained draws per chain with thinning set to one. Sampling guards checked an upper Gelman–Rubin bound below 1.01 and an effective sample size above 1,000.

Trace, density and autocorrelation diagnostics were accompanied by numerical summaries. The statistics are classical `coda` Gelman–Rubin diagnostics and effective-size estimates for means; they are not rank-normalised R-hat or bulk/tail effective sample sizes. Passing these checks supports computational stability but does not establish that the likelihood or independence assumptions are correct.

An independent R integration calculation checked conditional-model posterior means and marginal likelihoods. A JAGS product-space model-index calculation separately checked the close M1-versus-M2 comparison. The negligible M0 weight was evaluated through marginal likelihoods rather than inferred from zero sampled model visits.

## Main findings

### Sex adjustment changes the association

On the same 333 records, the estimated flipper slope is **39.93 g/mm** in M0 and **20.47 g/mm** in M1. A 10 mm flipper difference therefore corresponds to approximately **399 g** versus **205 g** in expected mass under the respective models.

M1 estimates a male–female contrast of **524.80 g**, with a **95% highest-density interval of 450.99–598.08 g**, at common species and flipper length. This is an adjusted observational association and does not establish causation.

### Model complexity remains uncertain

Under equal prior model probabilities and the baseline coefficient priors, the report gives:

| Model | Posterior probability |
| --- | ---: |
| M0 | Approximately zero, reported as 2.2571 × 10⁻³³ |
| M1 | 0.45045 |
| M2 | 0.54955 |

The M1-versus-M0 Bayes factor is approximately **2.00 × 10³²**, supporting sex adjustment within this candidate set and these priors. The M2-versus-M1 Bayes factor is only **1.22**, providing little separation between the two sex-adjusted models.

Doubling coefficient-prior standard deviations changes M2’s posterior weight from approximately **0.550 to 0.211**. A preference for simpler models also changes the ranking. The report therefore carries model uncertainty into predictions through model averaging.

### Fit measures describe the analysed sample

| Model | Records | In-sample RMSE in grams | Bayesian R² | In-sample 95% predictive coverage |
| --- | ---: | ---: | ---: | ---: |
| M0 | 333 | 371.1 | 0.784 | 95.2% |
| M1 | 333 | 293.4 | 0.864 | 94.9% |
| M2 | 333 | 291.1 | 0.866 | 94.9% |

These are fitted-data and posterior-predictive checks. No train/test split or held-out evaluation is reported, so they do not establish prediction accuracy for unseen data. Predictive coverage is also different from a coefficient’s highest-density interval.

For an Adelie penguin with 200 mm flippers, the baseline-prior model-averaged female mean is **3.640 kg**, with a **95% interval for the mean of 3.541–3.738 kg**. The corresponding **individual predictive interval is 3.060–4.233 kg**. The wider interval includes residual variation as well as uncertainty about parameters and models.

## Interpretation and limitations

The data are observational and geographically imbalanced: all observed Chinstrap records come from Dream Island and all Gentoo records from Biscoe Island. Species also have limited overlapping flipper-length ranges. These patterns restrict causal interpretation and the empirical support for some adjusted comparisons.

The models assume conditional independence, normal errors, shared residual variance and a common sex contrast. Possible nest, island and year dependence is not modelled. The report does not present robust-error models, species-specific error variances or held-out validation. Results are conditional on the selected models, priors and complete cases, and should not be generalised automatically to different populations or seasons.

## Portfolio scope and contribution

This was an individual RMIT course project. The portfolio demonstrates sample definition, Bayesian model comparison, uncertainty interpretation, diagnostic reasoning and technical communication using the completed coursework report as evidence.

The original report acknowledges ChatGPT assistance with dataset-source checking, preparation of R/JAGS and report-generation code, identifying assessment gaps, drafting explanations and arranging the report. This portfolio was prepared with AI assistance and preserves that disclosure. It does not independently certify personal review of every original computation.

All numerical results above are quoted from the report’s recorded execution. Portfolio preparation did not rerun the models or recreate the missing execution archive. This repository currently contains documentation rather than a verified runnable analysis. It excludes the original submission, student identifiers, course materials and datasets.

## Public references

- [Palmer Penguins dataset and attribution](https://allisonhorst.github.io/palmerpenguins/)
- [Gorman, Williams and Fraser 2014 ecological field study](https://doi.org/10.1371/journal.pone.0090081)
- [Horst, Hill and Gorman 2020 dataset reference](https://doi.org/10.5281/zenodo.3960218)
- [JAGS project](https://mcmc-jags.sourceforge.io/)
- [`rjags` package documentation](https://cran.r-project.org/package=rjags)
- [`coda` package documentation](https://cran.r-project.org/package=coda)
