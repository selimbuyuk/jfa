[![CRAN](https://img.shields.io/cran/v/jfa?color=yellow&label=CRAN&logo=r)](https://cran.r-project.org/package=jfa)
[![R_build_status](https://github.com/koenderks/jfa/workflows/Build/badge.svg)](https://github.com/koenderks/jfa/actions)
[![Codecov](https://codecov.io/gh/koenderks/jfa/branch/development/graph/badge.svg?token=ZoxIB8p8PW)](https://codecov.io/gh/koenderks/jfa)
[![Bugs](https://img.shields.io/github/issues/koenderks/jfa/bug?label=Bugs&logo=github&logoColor=%23FFF&color=brightgreen)](https://github.com/koenderks/jfa/issues?q=is%3Aopen+is%3Aissue+label%3Abug)
[![Monthly](https://cranlogs.r-pkg.org/badges/jfa?color=blue)](https://cranlogs.r-pkg.org)
[![Total](https://cranlogs.r-pkg.org/badges/grand-total/jfa?color=blue)](https://cranlogs.r-pkg.org)

# jfa: Bayesian and Classical Audit Sampling

<img src='https://github.com/koenderks/jfa/raw/development/man/figures/logo.png' width='149' height='173' alt='logo' align='right' margin-left='20' margin-right='20'/>

`jfa` is an R package for statistical audit sampling. The package provides functions for planning, performing, evaluating, and reporting an audit sample compliant with the International Standards on Auditing. Specifically, these functions implement standard audit sampling techniques for calculating sample sizes, selecting items from a population, and evaluating the misstatement from a data sample or from summary statistics. Additionally, the `jfa` package allows the user to create a prior probability distribution to perform Bayesian audit sampling using these functions.

The package and its intended workflow are also implemented with a graphical user interface in the Audit module of [JASP](https://jasp-stats.org), a free and open-source statistical software program.

## Overview

For complete documentation of `jfa`, visit the [package website](https://koenderks.github.io/jfa/) or download the [package manual](https://cran.r-project.org/package=jfa/jfa.pdf).

1. [Installation](#1-installation)
2. [Cheat sheet](#2-cheat-sheet)
3. [Benchmarks](#3-benchmarks)
4. [Statistical tables](#4-statistical-tables)
5. [Intended workflow](#5-intended-workflow)
6. [References](#6-references)
7. [Package statistics](#7-package-statistics) 
8. [Contributing](#8-contributing) 

## 1. Installation

The most recently released version of `jfa` can be downloaded from [CRAN](https://cran.r-project.org/package=jfa) by running the following command in R:

```r
install.packages('jfa')
```

Alternatively, you can download the development version from GitHub using:

```r
devtools::install_github('koenderks/jfa')
```

After installation, the `jfa` package can be loaded with:

```r
library(jfa)
```

## 2. Cheat sheet

The cheat sheet below can help you get started with the `jfa` package and its intended workflow. You can download a `pdf` version of the cheat sheet [here](https://github.com/koenderks/jfa/raw/development/man/figures/cheatsheet/cheatsheet.pdf).

<p align='center'><img src='https://github.com/koenderks/jfa/raw/development/man/figures/cheatsheet/cheatsheet.png' alt='cheatsheet' width='1000'></p>

## 3. Benchmarks

To validate the statistical results, `jfa`'s automated [unit tests](https://github.com/koenderks/jfa/tree/development/tests/testthat) regularly verify the main output from the package against the following benchmarks:

- [Audit Sampling: Audit Guide](https://future.aicpa.org/cpe-learning/publication/audit-sampling-audit-guide-OPL) (Appendix A and Appendix C)
- [AuditSampler](https://cplusglobal.wordpress.com/solutions/auditsampler-statistical-sampling-software/)
- [MUS](https://cran.r-project.org/package=MUS) (R package version 0.1.6)
- Touw, P., and Hoogduin, L. (2011). *Statistiek voor audit en controlling*. Boom uitgevers, Amsterdam.
- [SMASH21 + SMASH21-Bayes](https://steekproeven.eu/)

## 4. Statistical tables

Below you can find several informative tables that contain statistical sample sizes, upper limits, and Bayes factors. These tables are created using the `planning()` and `evaluation()` functions provided in the package.

*Sample sizes*

- [Sample sizes based on the Poisson distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaPoissonSampleSizes.pdf)
- [Sample sizes based on the binomial distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaBinomialSampleSizes.pdf)
- [Sample sizes based on the hypergeometric distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaHypergeometricSampleSizes.pdf)

*Upper limits*

- [Upper limits based on the Poisson distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaPoissonUpperBounds.pdf)
- [Upper limits based on the binomial distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaBinomialUpperBounds.pdf)
- [Upper limits based on the hypergeometric distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaHypergeometricUpperBounds.pdf)

*Bayes factors*

- [Bayes factors based on the gamma distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaPoissonBayesFactors.pdf)
- [Bayes factors based on the beta distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaBinomialBayesFactors.pdf)
- [Bayes factors based on the beta-binomial distribution](https://github.com/koenderks/jfa/raw/development/man/figures/tables/jfaHypergeometricBayesFactors.pdf)

## 5. Intended workflow

<p align='center'><img src='https://github.com/koenderks/jfa/raw/development/man/figures/readme/banner/jfaBanner.png' alt='banner'/></p>

Below you can find an explanation of the available functions in `jfa`, sorted by their occurrence in the standard audit sampling workflow. For detailed examples of how to use these functions, visit the [Get started](https://koenderks.github.io/jfa/articles/jfa.html) section on the package website.

- [`auditPrior()`](#create-a-prior-distribution-with-the-auditprior-function)
- [`planning()`](#plan-a-sample-with-the-planning-function)
- [`selection()`](#select-items-with-the-selection-function)
- [`evaluation()`](#evaluate-a-sample-with-the-evaluation-function)
- [`report()`](#create-a-report-with-the-report-function)

### Create a prior distribution with the `auditPrior()` function

[![Lifecycle: stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)

The `auditPrior()` function creates a prior distribution according to one of several methods, including a translation of the assessments of the inherent risk and control risk from the audit risk model. The function returns an object of class `jfaPrior` which can be used with associated `summary()` and `plot()` methods. Objects with class `jfaPrior` can also be used as input for the `prior` argument in other functions.

*Full function with default arguments:*

```r
auditPrior(method = 'none', likelihood = 'poisson', expected = 0, 
           conf.level = 0.95, materiality = NULL, N.units = NULL, 
           ir = NULL, cr = NULL, ub = NULL, p.hmin = NULL,
           x = NULL, n = NULL, factor = NULL, alpha = NULL, beta = NULL)
```

*Supported options for the `method` argument:*

| `method` | Description | Required arguments | Reference |
| :----------- | :----------- | :----------- | :----------- |
| `none` | No prior information | | Derks et al. (2021) |
| `arm` | Translates risk assessments (ARM) | `materiality`, `ir` and `cr` | Derks et al. (2021) |
| `bram` | Bayesian risk assessment model (BRAM) | `ub` | Touw and Hoogduin (2011) |
| `median` | Equal prior probabilities for (in)tolerable misstatement | `materiality` | Derks et al. (2021) |
| `hypotheses` | Custom prior probabilities for (in)tolerable misstatement | `materiality` and `p.hmin` | Derks et al. (2021) |
| `sample` | Earlier sample | `x` and `n` | Derks et al. (2021) |
| `factor` | Weighted earlier sample | `x`, `n`, and `factor` | Derks et al. (2021) |
| `custom` | Manually set the prior parameters | `alpha` and `beta` | |

*Supported options for the `likelihood` argument:*

| `likelihood` | Description | Reference |
| :----------- | :----------- | :----------- |
| `poisson` | Gamma prior distribution (+ Poisson likelihood) | Stewart (2013) |
| `binomial` | Beta prior distribution (+ binomial likelihood) | Steele (1992) |
| `hypergeometric` | Beta-binomial prior distribution (+ hypergeometric likelihood) | Dyer and Pierce (1991) |

*Example usage:*

```r
# A noninformative gamma prior distribution 
x <- auditPrior(method = 'none', likelihood = 'poisson')

# A beta(1, 10) prior distribution 
x <- auditPrior(method = 'custom', likelihood = 'binomial', alpha = 1, beta = 10)

summary(x) # Prints information about the prior distribution
```

### Plan a sample with the `planning()` function

[![Lifecycle: stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)

The `planning()` function calculates the minimum sample size for a statistical audit sample based on the Poisson, binomial, or hypergeometric likelihood. The function returns an object of class `jfaPlanning` which can be used with associated `summary()` and `plot()` methods. To perform Bayesian planning, the input for the `prior` argument can be an object of class `jfaPrior` as returned by the `auditPrior()` function, or an object of class `jfaPosterior` as returned by the `evaluation()` function.

*Full function with default arguments:*

```r
planning(materiality = NULL, min.precision = NULL, expected = 0,
         likelihood = 'poisson', conf.level = 0.95, N.units = NULL,
         by = 1, max = 5000, prior = FALSE)
```

*Supported options for the `likelihood` argument:*

| `likelihood` | Description | Reference |
| :----------- | :----------- | :----------- |
| `poisson` | Poisson likelihood | Stewart (2012) |
| `binomial` | Binomial likelihood | Stewart (2012) |
| `hypergeometric` | Hypergeometric likelihood | Stewart (2012) |

*Example usage:*

```r
# Classical planning using Poisson likelihood
x <- planning(materiality = 0.03, likelihood = 'poisson')

# Bayesian planning using noninformative gamma prior
x <- planning(materiality = 0.03, likelihood = 'poisson', prior = TRUE)

# Bayesian planning using a beta(1, 10) prior
x <- planning(materiality = 0.03, 
              prior = auditPrior(method = 'custom', likelihood = 'binomial', alpha = 1, beta = 10))

summary(x) # Prints information about the planning
```

### Select items with the `selection()` function

[![Lifecycle: stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)

The `selection()` function takes a data frame and performs statistical sampling according to one of three algorithms: random sampling, cell sampling, or fixed interval sampling in combination with either record sampling or monetary unit sampling. The function returns an object of class `jfaSelection` which can be used with associated `summary()` and `plot()` methods. The input for the `size` argument can be an object of class `jfaPlanning` as returned by the `planning()` function.

*Full function with default arguments:*

```r
selection(data, size, units = 'items', method = 'random', values = NULL,
          start = 1, order = TRUE, decreasing = FALSE, replace = FALSE)
```

*Supported options for the `units` argument:*

| `units` | Description | Required arguments |  Reference |
| :----------- | :----------- | :----------- | :----------- |
| `items` | Sampling units are items (rows) | | Leslie, Teitlebaum, and Anderson (1979) |
| `mus` | Sampling units are monetary units | `values` | Leslie, Teitlebaum, and Anderson (1979) |

*Supported options for the `method` argument:*

| `method` | Description | Required arguments |
| :----------- | :----------- | :----------- |
| `random` | Select random units without the use of an interval | |
| `cell` | Select a random unit from every interval | |
| `interval` | Select a fixed unit from every interval | `start` |

*Example usage:*

```r
# Selection using random record sampling
x <- selection(data = BuildIt, size = 100, units = 'items', method = 'random')

# Selection using fixed interval MUS
x <- selection(data = BuildIt, size = 100, units = 'mus', method = 'interval')

summary(x) # Prints information about the selection
```

### Evaluate a sample with the `evaluation()` function

[![Lifecycle: stable](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html#stable)

The `evaluation()` function takes a sample or summary statistics of the sample and performs evaluation according to the specified method and sampling objectives. The function returns an object of class `jfaEvalution` which can be used with associated `summary()` and `plot()` methods. To perform Bayesian evaluation, the input for the `prior` argument can be an object of class `jfaPrior` as returned by the `auditPrior()` function, or an object of class `jfaPosterior` as returned by the `evaluation()` function.

*Full function with default arguments:*

```r
evaluation(materiality = NULL, min.precision = NULL, method = 'poisson',
           conf.level = 0.95, data = NULL, values = NULL, values.audit = NULL,
           times = NULL, x = NULL, n = NULL, N.units = NULL, N.items = NULL, 
           r.delta = 2.7, m.type = 'accounts', cs.a = 1, cs.b = 3, cs.mu = 0.5, 
           prior = FALSE)
```

*Supported options for the `method` argument:*

| `method` | Description | Required arguments | Reference |
| :----------- | :----------- | :----------- | :----------- |
| `poisson` | Poisson likelihood | | Stewart (2012) |
| `binomial` | Binomial likelihood | | Stewart (2012) |
| `hypergeometric` | Hypergeometric likelihood | `N.units` | Stewart (2012) |
| `stringer` | Classical Stringer bound | | Bickel (1992) |
| `stringer.meikle` | Stringer bound with Meikle's correction | | Meikle (1972) |
| `stringer.lta` | Stringer bound with LTA correction | | Leslie, Teitlebaum, & Anderson (1979) |
| `stringer.pvz` | Modified Stringer bound | | Pap and van Zuijlen (1996) |
| `rohrbach` | Rohrbach's augmented variance estimator | `r.delta` | Rohrbach (1993) |
| `moment` | Modified moment bound | `m.type` | Dworin and Grimlund (1984) |
| `coxsnell` | Cox and Snell bound | `cs.a`, `cs.b`, and `cs.mu` | Cox and Snell (1979) |
| `direct` | Direct estimator | `N.items` and `N.units` | Touw and Hoogduin (2011) |
| `difference` | Difference estimator | `N.items` | Touw and Hoogduin (2011) |
| `quotient` | Quotient estimator | `N.items` | Touw and Hoogduin (2011) |
| `regression` | Regression estimator | `N.items` and `N.units` | Touw and Hoogduin (2011) |

*Example usage:*

```r
# Classical evaluation using the Poisson likelihood (and summary statistics)
x <- evaluation(materiality = 0.03, x = 1, n = 100, method = 'poisson')

# Bayesian evaluation using a noninformative gamma prior
x <- evaluation(materiality = 0.03, x = 1, n = 100, method = 'poisson', prior = TRUE)

# Bayesian evaluation using a beta(1, 10) prior
x <- evaluation(materiality = 0.03, x = 1, n = 100, 
                prior = auditPrior(method = 'custom', likelihood = 'binomial', alpha = 1, beta = 10))

summary(x) # Prints information about the evaluation
```

### Create a report with the `report()` function

[![Lifecycle: experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)

The `report()` function takes an object of class `jfaEvaluation` as returned by the `evaluation()` function and automatically creates a `html` or `pdf` report containing the analysis results and their interpretation.

*Full function with default arguments:*

```r
report(object, file = 'report.html', format = 'html_document')
```

*Example usage:*

```r
# Generate an automatic report
report(object = x, file = 'myReport.html')
```

For an example report, see the following [link](https://github.com/koenderks/jfa/raw/development/man/figures/readme/report/report.pdf).

## 6. References

- Bickel, P. J. (1992). Inference and auditing: The Stringer bound. *International Statistical Review*, 60(2), 197–209. - [View online](https://www.jstor.org/stable/1403650)
- Cox, D. R., & Snell, E. J. (1979). On sampling and the estimation of rare errors. *Biometrika*, 66(1), 125-132. - [View online](https://doi.org/10.1093/biomet/66.1.125)
- Derks, K. (2021). jfa: Bayesian and classical audit sampling. R package version 0.6.0. - [View online](https://cran.r-project.org/package=jfa)
- Derks, K., de Swart, J., van Batenburg, P., Wagenmakers, E.-J., & Wetzels, R. (2021). Priors in a Bayesian audit: How integration of existing information into the prior distribution can improve audit transparency and efficiency. *International Journal of Auditing*, 1-16. - [View online](https://doi.org/10.1111/ijau.12240)
- Dworin, L. D. and Grimlund, R. A. (1984). Dollar-unit sampling for accounts receivable and inventory. *The Accounting Review*, 59(2), 218–241. - [View online](https://www.jstor.org/stable/247296)
- Dyer, D., & Pierce, R. L. (1993). On the choice of the prior distribution in hypergeometric sampling. *Communications in Statistics - Theory and Methods*, 22(8), 2125-2146. - [View online](https://www.tandfonline.com/doi/abs/10.1080/03610929308831139)
- International Auditing and Assurance Standards Board (IAASB). (2018). *Handbook of international quality control, auditing review, other assurance, and related services pronouncements (Vol. I)*. New York: International Federation of Accountants.
- Meikle, G. R. (1972). *Statistical Sampling in an Audit Context*. Canadian Institute of Chartered Accountants.
- Leslie, D. A., Teitlebaum, A. D., & Anderson, R. J. (1979). *Dollar-unit Sampling: A Practical Guide for Auditors*. London: Pitman.
- Pap, G., & van Zuijlen, M. C. (1996). On the asymptotic behaviour of the Stringer bound. *Statistica Neerlandica*, 50(3), 367-389. - [View online](https://doi.org/10.1111/j.1467-9574.1996.tb01503.x)
- Rohrbach, K. J. (1993). Variance augmentation to achieve nominal coverage probability in sampling from audit populations. *Auditing: A Journal of Practice & Theory*, 12(2), 79-97.
- Steele, A. (1992). *Audit Risk and Audit Evidence: The Bayesian Approach to Statistical Auditing*. San Diego: Academic Press.
- Stewart, T. R. (2012). *Technical Notes on the AICPA Audit Guide Audit Sampling*. American Institute of Certified Public Accountants, New York. - [View online](https://www.aicpa.org/content/dam/aicpa/publications/accountingauditing/keytopics/downloadabledocuments/sampling-guide-technical-notes.pdf)
- Stewart, T. R. (2013). *A Bayesian Audit Assurance Model with Application to the Component Materiality problem in Group Audits.* VU University, Amsterdam. - [View online](https://research.vu.nl/en/publications/a-bayesian-audit-assurance-model-with-application-to-the-componen)
- Talens, E. (2005). *Statistical Auditing and the AOQL-method*. University of Groningen, Groningen. - [View online](https://research.rug.nl/en/publications/statistical-auditing-and-the-aoql-method)
- Touw, P., and Hoogduin, L. (2011). *Statistiek voor Audit en Controlling*. Boom uitgevers, Amsterdam.

## 7. Package statistics

<img src='https://github.com/koenderks/jfa/raw/development/man/figures/readme/downloads/downloads.svg' width='50%' /><img src='https://github.com/koenderks/jfa/raw/development/man/figures/readme/worldmap/worldmap.svg' width='50%' />

## 8. Contributing

`jfa` is an open-source project that aims to be useful for the audit community. Your help in benchmarking and extending `jfa` is therefore greatly appreciated. Contributing to `jfa` does not have to take much time or knowledge, and there is extensive information available about it on the [Wiki](https://github.com/koenderks/jfa/wiki) of this repository.

If you are willing to contribute to the improvement of the package by adding a benchmark, please check out the Wiki page on [how to contribute a benchmark to jfa](https://github.com/koenderks/jfa/wiki/Benchmarks). If you are willing to contribute to the improvement of the package by adding a new statistical method, please check the Wiki page on [how to contribute a new method to jfa](https://github.com/koenderks/jfa/wiki/Methods).
