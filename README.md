# Missing Data, Data Imputation
> In statistics, missing data, or missing values, occur when no data value is stored for the variable in an observation ([Wiki](https://en.wikipedia.org/wiki/Missing_data))

- **Overview**
  - A free book on data imputation by the author of [mice](https://stefvanbuuren.name/mice/) package:  
    [Flexible Imputation of Missing Data](https://stefvanbuuren.name/fimd/) (2018) *Stef van Buuren*
  - [Missing-data imputation](www.stat.columbia.edu/~gelman/arm/missing.pdf)(Ch. 25) of [Data Analysis Using Regression and Multilevel/Hierarchical Models](http://www.stat.columbia.edu/~gelman/arm/) (2006) ' *Andrew Gelman, Jennifer Hill*

### Types of missing data ([Wiki](https://en.wikipedia.org/wiki/Missing_data#Types))
  - Missed completely at random
  - Missed at random
  - Missed data that depends on unobserved variables
  - Missed data that depends on the missing value itself

### Discarding data
- **Listwise deletion** Complete-case analysis
  - Samples (rows) are removed from a dataset if they have missing values. Probably the most simple and popular approach. Often done automatically by many ML packages
  - When dealing with big number of variables that have missing values, the number of samples after deletion can be too small
  - May lead to biased estimates. Also smaller sample size increases standard errors
- **Available-case analysis** Complete-variables analysis
  - Excluding variables from data if their missing-values rate is lower than some threshold

### Imputation ([Wiki](https://en.wikipedia.org/wiki/Imputation_(statistics)))
> Whenever a single imputation strategy is used, the standard errors of estimates tend to be too low. The intuition here is that we have substantial uncertainty about the missing values, but by choosing a single imputation we inessence pretend that we know the true value with certainty ([Data Analysis Using Regression and Multilevel/Hierarchical Models](www.stat.columbia.edu/~gelman/arm/missing.pdf))

- **Mean/Mode Replacement**
  - Replaces missing values with a variable (column) mean, mode or median
  - Distorts a probability distribution of an imputed variable
  - Distorts relationship between variables
- **LOCF** Last Observation Carried Forward imputation ([Wiki](https://en.wikipedia.org/wiki/Analysis_of_clinical_trials#Last_observation_carried_forward))
  - In time-series data the last observed value before a missing one is "carried forward" to fill in the blank points
  - [Does analysis using “last observation carried forward” introduce bias in dementia research?]() *Frank J. Molnar, Brian Hutton, Dean Fergusson*
- **Indicator variables**
  - Extra category that indicates missingness of a variable
  - Extra binary indicator variable used together with a variable that includes  missing data (works with continuous data too)
- **Regression Imputation**
  - A regression model is created on a variable with missing values, then used to predict blank points
  - Deterministic regression imputation uses the original prediction of the regression model to impute missing values
  - Stochastic regression imputation adds random error
  - Article about the regression imputation method with examples:  
    [Regression Imputation (Stochastic vs. Deterministic & R Example)](https://statisticsglobe.com/regression-imputation-stochastic-vs-deterministic/) *Statistics Globe*
- **Iterative Regression Imputation**
  - When multiple variables have missing values, IRI imputes them iteratively: using non-missing variables first to impute the first missing variable, then using the imputed variable together with non-missing predictors to predict missing values of the second one, etc
- **SRMI** Sequential Regression Multivariate Imputation
  - [A Multivariate Technique for Multiply Imputing Missing Values Using a Sequence of Regression Models](https://pdfs.semanticscholar.org/13b3/0e35b9a54dad07094cfe4f50d40ff15d8370.pdf) (2001) *Trivellore E. Raghunathan, James M. Lepkowski, John Van Hoewyk, Peter Solenberger*
- **Cold-deck Imputation**
  - Impute missing data using previously collected datasets
- **Hot-deck Imputation**
  - For each sample with a missing value, find a similar complete-case sample in the same dataset and use it for imputation
  - Uses a scoring function to measure similarity
  - [A Review of Hot Deck Imputation for Survey Non-response](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3130338/) (2010) *Rebecca R. Andridge, Roderick J. A. Little*
- **KNN** k-Nearest Neighbors
- **Model-based Imputation**
  - When something is known about why missing data exist, it's possible to directly model the missingness
- **Multiple Imputation** ([Wiki](https://en.wikipedia.org/wiki/Imputation_(statistics)#Multiple_imputation))
  - Drawing imputed values multiple times from some distribution. Then each realization of imputed data is analysed. Aggregated results from all realizations are used to get uncertainty estimation.
  - [Multiple Imputation for Nonresponse in Surveys](https://www.onlinelibrary.wiley.com/doi/pdf/10.1002/9780470316696.fmatter) (1987) *Donald B. Rubin*
  - [Analyzing Incomplete Political Science Data: An Alternative Algorithm forMultiple Imputation] (2001) *Gary King, James Honaker, Anne Joseph, Kenneth Scheve*
- **MICE** Multivariate Imputation by Chained Equations ([Homepage](https://stefvanbuuren.name/mice/), [Code](https://github.com/stefvanbuuren/mice), [CRAN](https://cran.r-project.org/web/packages/mice/))
  - [mice: Multivariate Imputation by Chained Equations in R](https://www.jstatsoft.org/article/view/v045i03) (2011) *Stef van Buuren, Karin Groothuis-Oudshoorn*
- **MissForest** ([Code](https://github.com/stekhoven/missForest), [CRAN](https://cran.r-project.org/web/packages/missForest/))
  - [MissForest - nonparametric missing value imputation for mixed-type data](https://stat.ethz.ch/Manuscripts/buhlmann/missforest-advacc.pdf) (2011) *Daniel J.Stekhoven, Peter Buhlmann*
- **Optimal Transport** ([Code](https://github.com/BorisMuzellec/MissingDataOT))
  - [Missing Data Imputation using Optimal Transport](https://arxiv.org/abs/2002.03860) (2020) *Boris Muzellec, Julie Josse, Claire Boyer, Marco Cuturi*
- **Autoencoders**

### Other methods, packages
- **MIDAS** Multiple Imputation with Denoising Autoencoders ([Code](https://github.com/Oracen/MIDAS))
- **Impute.jl** ([Code](https://github.com/invenia/Impute.jl))
