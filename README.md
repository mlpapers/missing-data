# Missing Data, Data Imputation
> In statistics, missing data, or missing values, occur when no data value is stored for the variable in an observation ([Wiki](https://en.wikipedia.org/wiki/Missing_data))

- **Overview**
  - A free book on data imputation by the author of [mice](https://stefvanbuuren.name/mice/) package:  
    [Flexible Imputation of Missing Data](https://stefvanbuuren.name/fimd/) (2018) *Stef van Buuren*

### Imputation methods
- **Listwise deletion**
  - Samples (rows) are removed from a dataset if they have missing values. Probably the most simple and popular approach. 
- **Mean/Mode Replacement**
  - Replace with missing values with variable (column) mean, mode or median
- **LOCF** Last Observation Carried Forward imputation ([Wiki](https://en.wikipedia.org/wiki/Analysis_of_clinical_trials#Last_observation_carried_forward))
  - In time-series data the last observed value before a missing one is "carried forward" to fill in the blank points
  - [Does analysis using “last observation carried forward” introduce bias in dementia research?]() *Frank J. Molnar, Brian Hutton, Dean Fergusson*
- **Regression Imputation**
  - A regression model is created on a variable with missing values, then used to predict blank points
  - Deterministic regression imputation uses the original prediction of the regression model to impute missing values
  - Stochastic regression imputation adds random error
  - Article about the regression imputation method with examples:  
    [Regression Imputation (Stochastic vs. Deterministic & R Example)](https://statisticsglobe.com/regression-imputation-stochastic-vs-deterministic/) *Statistics Globe*

- **Hot-deck Imputation**
  - [A Review of Hot Deck Imputation for Survey Non-response](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3130338/) (2010) *Rebecca R. Andridge, Roderick J. A. Little*
- **KNN** k-Nearest Neighbors
- **Multiple Imputation**
- **Optimal Transport** ([Code](https://github.com/BorisMuzellec/MissingDataOT))
  - [Missing Data Imputation using Optimal Transport](https://arxiv.org/abs/2002.03860) (2020) *Boris Muzellec, Julie Josse, Claire Boyer, Marco Cuturi*
- **MICE** Multivariate Imputation by Chained Equations ([Homepage](https://stefvanbuuren.name/mice/), [Code](https://github.com/stefvanbuuren/mice), [CRAN](https://cran.r-project.org/web/packages/mice/))
  - [mice: Multivariate Imputation by Chained Equations in R](https://www.jstatsoft.org/article/view/v045i03) (2011) *Stef van Buuren, Karin Groothuis-Oudshoorn*
- **MissForest** ([Code](https://github.com/stekhoven/missForest), [CRAN](https://cran.r-project.org/web/packages/missForest/))
  - [MissForest - nonparametric missing value imputation for mixed-type data](https://stat.ethz.ch/Manuscripts/buhlmann/missforest-advacc.pdf) (2011) *Daniel J.Stekhoven, Peter Buhlmann*
- **Autoencoders**

### Other methods, packages
- **MIDAS** Multiple Imputation with Denoising Autoencoders ([Code](https://github.com/Oracen/MIDAS))
- **Impute.jl** ([Code](https://github.com/invenia/Impute.jl))
