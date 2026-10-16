# econ3916-lab07-bootstrapping
Lab 07 Submission

# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective
I measured how much an estimate would change from sample to sample, first with textbook formulas and then with the bootstrap, and tested when each method can be trusted.

## Methodology
- Loaded the UCI Adult Census Income dataset (32,561 respondents).
- Separated the standard deviation of the data from the standard error of an estimate, and checked the s/√n relationship across four sample sizes.
- Built parametric confidence intervals from the Central Limit Theorem and compared how quickly the CLT takes hold for age versus capital gains.
- Ran the bootstrap by hand, then repeated it with `scipy.stats.bootstrap`.
- Investigated a degenerate case: the bootstrap standard error of the median age.
- Compared percentile and BCa bootstrap intervals on a heavily skewed variable.
- Bootstrapped a two-sample difference in mean weekly hours worked.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked its output against my own intervals.
- Ran a coverage simulation on lognormal data at n = 50 to see how often nominal 95% intervals actually contain the true value, for both the mean and the median.

## Key Findings
- **Standard deviation and standard error measure different things.** The standard deviation describes the spread of the data; the standard error describes the spread of an estimate. Across four sample sizes, the standard error shrank in line with s/√n.
- **The CLT converges at different speeds for different variables.** For age, the sampling distribution of the mean looked normal quickly. For capital gains, which is heavily skewed, it took much larger samples.
- **A bootstrap standard error of zero can be correct.** The bootstrap SE of the median of 32,561 whole-number ages came out to exactly 0.0000. With that many tied values, every resample returns the same median. The bootstrap was reporting a real property of the data, not failing.
- **Mean coverage: the two methods are indistinguishable.** In the lognormal simulation at n = 50, the nominal 95% parametric interval for the mean covered [YOUR VALUE]% and the percentile bootstrap covered [YOUR VALUE]%. The gap between them falls inside the Monte Carlo standard error of about 1.3 points, so I can't separate the two methods here. Both under-cover slightly.
- **Median coverage: the bootstrap holds up and the formula does not.** The mean-centred parametric interval covered the true median only about [YOUR VALUE]% of the time, while the bootstrap stayed near its nominal 95%. The bootstrap's advantage shows up when there is no simple formula for the statistic.
