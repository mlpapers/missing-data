# Missing Data and Imputation

## Overviews

- **[Flexible Imputation of Missing Data](https://www.routledge.com/Flexible-Imputation-of-Missing-Data-Second-Edition/vanBuuren/p/book/9781138588318)** — van Buuren (2018, 2nd ed.). Missingness assumptions, multiple imputation, diagnostics, and applications. [Online chapters](https://github.com/stefvanbuuren/fimd) and [book source](https://github.com/stefvanbuuren/fimdbook).
- **[Missing-data imputation](https://www.stat.columbia.edu/~gelman/arm/missing.pdf)** — Gelman & Hill (2007), Chapter 25. Compares deletion, simple replacements, regression, and model-based imputation; explains why treating filled values as observed understates uncertainty.
- **[Missing Data: Our View of the State of the Art](https://stat.ethz.ch/education/semesters/ss2013/ams/paper/missing_data_1.pdf)** — Schafer & Graham (2002). Reviews missingness assumptions, likelihood inference, and multiple imputation. [Pigott (2001)](https://doi.org/10.1076/edre.7.4.353.8937) compares these with deletion and single-value methods.

## Missingness Mechanisms and Assumptions

- **[Missing completely at random (MCAR)](https://stefvanbuuren.github.io/fimd/sec-MCAR.html)** — Missingness probabilities do not depend on observed or unobserved data values. Complete cases then form a random subsample, with reduced information.
- **[Missing at random (MAR)](https://stefvanbuuren.github.io/fimd/sec-MCAR.html)** — Given the observed data, missingness does not additionally depend on the missing values. MAR permits systematic missingness explained by observed variables; it does not mean entries disappear uniformly.
- **[Missing not at random (MNAR)](https://stefvanbuuren.github.io/fimd/sec-MCAR.html)** — Missingness still depends on unobserved values after conditioning on observed data. Distinguishing MAR from MNAR generally requires assumptions beyond the observed data.
- **[Ignorability](https://dash.harvard.edu/entities/publication/73120378-8764-6bd4-e053-0100007fdf3b)** — Rubin (1976). MAR and distinct data/missingness parameters permit ignoring the missingness model in direct-likelihood inference. This does not justify arbitrary deletion or replacement rules.
- **[MNAR sensitivity analysis](https://amices.org/mice/reference/mice.impute.mnar.html)** — Delta-adjusted imputation shifts conditional distributions away from MAR through user-specified sensitivity parameters. Vary plausible departures; the observed data alone do not identify those shifts.
- **[Graphical missing-data recovery](https://arxiv.org/abs/1801.03583)** — 2018. Uses graphs to express missingness assumptions and derive recoverability and testability conditions, including some MNAR cases. Recovery depends on the graph and target quantity.

## Deletion and Simple Imputation

- **[Complete-case analysis](https://stefvanbuuren.github.io/fimd/sec-simplesolutions.html)** — Uses rows complete on the variables needed for an analysis. MCAR is a sufficient, not necessary, condition for validity; selection can bias estimates and discarding rows reduces information.
- **[Available-case / pairwise deletion](https://stefvanbuuren.github.io/fimd/sec-simplesolutions.html)** — Uses all observed values for each statistic, so covariances may use different subsets. The resulting covariance matrix need not be positive semidefinite. This is not deletion of columns.
- **[Mean, median, and mode replacement](https://scikit-learn.org/stable/modules/impute.html#univariate-feature-imputation)** — Simple column-wise baselines. Deterministic fills do not represent imputation uncertainty; mean replacement reduces variance and can distort correlations. [Statistical limitations](https://stefvanbuuren.github.io/fimd/sec-simplesolutions.html).
- **[Regression imputation](https://stefvanbuuren.github.io/fimd/sec-simplesolutions.html)** — Predicts a missing variable from observed predictors. Deterministic predictions suppress residual variation; stochastic regression adds residual draws. Multiple imputation also accounts for parameter uncertainty.
- **[Hot-deck and cold-deck imputation](https://pmc.ncbi.nlm.nih.gov/articles/PMC3130338/)** — Andridge & Little (2010). Hot-deck methods draw observed values from eligible donors in the current sample; cold-deck methods use an external source. Donor selection determines which relationships are preserved.
- **[Predictive mean matching](https://stefvanbuuren.github.io/fimd/sec-pmm.html)** — Selects donors with similar predicted outcomes, then copies an observed donor value. Preserves observed support; results depend on the prediction model and donor pool.
- **[K-nearest-neighbor imputation](https://scikit-learn.org/stable/modules/impute.html#nearest-neighbors-imputation)** — Fills each feature from nearby samples that observed it. Distances use jointly observed coordinates; scaling and sparse overlap affect which donors are selected.

## Likelihood and Multiple Imputation

- **[Expectation-maximization (EM)](https://web.mit.edu/6.435/www/Dempster77.pdf)** — Dempster, Laird & Rubin (1977). Alternates expected complete-data log likelihood and parameter updates. Fits an observed-data model; it is not itself a procedure for producing multiple completed datasets.
- **[Multiple imputation](https://doi.org/10.1002/9780470316696)** — Rubin (1987). Generates multiple plausible completions, analyzes each, and combines estimates with within- and between-imputation variance. Pool analysis results, not completed datasets. [Pooling](https://amices.org/mice/reference/pool.html).
- **[Imputation–analysis compatibility](https://arxiv.org/abs/1911.09980)** — 2019/2020. Rubin’s rules can fail when imputation and analysis models are uncongenial. Bartlett and Hughes find valid bootstrap-before-imputation variants under consistent point estimation; resampling cannot fix a biased point estimate.
- **[Sequential regression multivariate imputation](https://www150.statcan.gc.ca/n1/pub/12-001-x/2001001/article/5857-eng.pdf)** — Raghunathan et al. (2001). Cycles through variable-specific regression models and draws from predictive distributions, accommodating different variable types and logical constraints.
- **[Fully conditional specification](https://doi.org/10.1177/0962280206074463)** — van Buuren (2007). Specifies an imputation model for each incomplete variable. Flexible conditional models need not correspond to one compatible joint distribution.
- **[MICE](https://www.jstatsoft.org/article/view/v045i03)** — van Buuren & Groothuis-Oudshoorn (2011). Implements chained equations with variable-specific methods, predictor selection, and diagnostics. [Azur et al. (2011)](https://doi.org/10.1002/mpr.329) explain the workflow and assumptions.
- **[Joint-model multiple imputation](https://gking.harvard.edu/files/evil.pdf)** — King et al. (2001). Develops an alternative computational approach to multiple imputation for incomplete multivariate data. [Amelia II](https://www.jstatsoft.org/article/view/v045i07) — Honaker et al. (2011) — uses bootstrap-based EM.

## Tabular and Low-Rank Methods

- **[missForest](https://doi.org/10.1093/bioinformatics/btr597)** — Stekhoven & Bühlmann (2012; preprint 2011). Iteratively fits random forests to incomplete columns, supporting mixed numeric/categorical data. Out-of-bag error estimates imputation error, not inferential confidence intervals. [Paper](https://stat.ethz.ch/Manuscripts/buhlmann/missforest-advacc.pdf).
- **[HyperImpute](https://proceedings.mlr.press/v162/jarrett22a.html)** — Jarrett et al. (2022). Extends iterative imputation with automatic selection of each column's prediction model and hyperparameters. Model search is part of fitting and must stay inside evaluation folds.
- **[SoftImpute](https://jmlr.org/papers/v11/mazumder10a.html)** — Mazumder, Hastie & Tibshirani (2010). Fits a low-rank matrix through nuclear-norm regularization and repeated soft-thresholded SVD. Suits shared latent structure; low rank alone does not resolve selective missingness.
- **[Optimal-transport imputation](https://proceedings.mlr.press/v119/muzellec20a.html)** — Muzellec et al. (2020). Optimizes missing entries by matching distributions of imputed batches with Sinkhorn divergences. Can learn an imputation function for new observations. [Code](https://github.com/BorisMuzellec/MissingDataOT).

## Deep Generative and Pretrained Imputers

- **[Autoencoders for incomplete records](https://psb.stanford.edu/psb-online/proceedings/psb17/beaulieujones.pdf)** — Beaulieu-Jones & Moore (2017). Evaluates autoencoder imputation on ALS trial data under simulated missingness, measuring reconstruction and progression prediction separately.
- **[MIDA](https://arxiv.org/abs/1705.02737)** — Gondara & Wang (2018; preprint 2017). Uses overcomplete denoising autoencoders for multiple imputation of mixed data. A separate method from Lall & Robinson's MIDAS software.
- **[Monte Carlo dropout autoencoders](https://arxiv.org/abs/2005.06173)** — Miok et al. (2020). Uses dropout within autoencoder and variational-autoencoder models to generate repeated imputations; evaluates reconstruction error and predictive similarity.
- **[GAIN](https://proceedings.mlr.press/v80/yoon18a.html)** — Yoon, Jordon & van der Schaar (2018). A generator fills missing entries; a discriminator predicts which entries were observed, aided by a partial missingness hint. The paper's identifiability result assumes MCAR.
- **[MIWAE](https://proceedings.mlr.press/v97/mattei19a.html)** — Mattei & Frellsen (2019). Trains a latent-variable model on incomplete data using an importance-weighted bound on observed-data likelihood under MAR. Supports Monte Carlo single and multiple imputations.
- **[not-MIWAE](https://arxiv.org/abs/2006.12871)** — Ipsen, Mattei & Frellsen (2021; preprint 2020). Jointly models values and missingness with importance-weighted variational inference. MNAR modeling relies on the specified mechanism; neural capacity does not establish identification.
- **[TabImpute and pattern-specific transformers](https://arxiv.org/abs/2510.02625v6)** — Feitelberg et al. (2025/2026, preprint). Pretrains imputers on synthetic tables with configurable missingness mechanisms. The default TabImpute uses MCAR training; specialists target particular patterns.
- **[ReMasker](https://arxiv.org/abs/2309.13793)** — 2023. Randomly masks additional observed entries and trains a masked autoencoder to reconstruct them, then imputes naturally missing values; the training task uses available table entries.
- **[MissDiff](https://arxiv.org/abs/2307.00467)** — 2023. Trains diffusion models directly on incomplete data by masking the denoising score-matching loss. Avoids first filling every missing entry with a separate imputer.

## Time-Series and Sensor Imputation

- **[Last observation carried forward](https://doi.org/10.1503/cmaj.080820)** — Molnar, Hutton & Fergusson (2008). Repeats the latest observed value across a gap. Assumes no change during that interval; bias can operate in either direction. [Limitations](https://stefvanbuuren.github.io/fimd/sec-simplesolutions.html).
- **[M-RNN](https://arxiv.org/abs/1711.08742)** — Yoon, Zame & van der Schaar (2019; preprint 2017). Combines interpolation within temporal streams with imputation across variables using a multidirectional recurrent network.
- **[BRITS](https://arxiv.org/abs/1805.10572)** — Cao et al. (2018). Learns missing values within bidirectional recurrent computation, combining temporal and cross-feature estimates. Uses observations on both sides of a gap, so its full form requires future context.
- **[GP-VAE](https://proceedings.mlr.press/v108/fortuin20a.html)** — Fortuin et al. (2020; preprint 2019). Places a Gaussian-process prior over a low-dimensional latent trajectory and decodes it into observations. Combines temporal structure with probabilistic imputation.
- **[CSDI](https://arxiv.org/abs/2107.03502)** — Tashiro et al. (2021). Trains conditional score-based diffusion models to sample missing time-series values given observations. Self-supervised masking creates training targets from observed entries. [Code](https://github.com/ermongroup/CSDI).
- **[SAITS](https://arxiv.org/abs/2202.08516)** — Du, Cote & Liu (2023; preprint 2022). Combines two diagonally masked self-attention blocks with learned weights, using reconstruction and masked-imputation objectives. [Code](https://github.com/WenjieDu/SAITS).
- **[GRIN](https://arxiv.org/abs/2108.00298)** — Cini, Marisca & Alippi (2022; preprint 2021). Uses graph message passing and recurrent processing to impute multivariate sensor streams. Exploits relations between sensors as well as temporal dependencies. [Code](https://github.com/Graph-Machine-Learning-Group/grin).

## Prediction with Missing Inputs

- **[Missingness indicators](https://scikit-learn.org/stable/modules/impute.html#marking-imputed-values)** — Binary masks preserve which inputs were missing after filling them. They can help prediction; adding indicators does not generally repair biased coefficient estimates. [Inference caveat](https://stefvanbuuren.github.io/fimd/sec-simplesolutions.html).
- **[RNNs with missingness indicators](https://proceedings.mlr.press/v56/Lipton16.html)** — Lipton, Kale & Wetzel (2016). Studies diagnosis prediction from irregular clinical measurements and their missingness patterns. The objective is supervised prediction, not recovering every absent measurement.
- **[GRU-D](https://www.nature.com/articles/s41598-018-24271-9)** — Che et al. (2018). Incorporates observation masks, elapsed times, and learned decays of inputs and hidden states into a recurrent predictor. Uses informative missingness directly.
- **[NeuMiss](https://proceedings.neurips.cc/paper_files/paper/2020/hash/42ae1544956fbe6e09242e6cd752444c-Abstract.html)** — Le Morvan et al. (2020). Derives a prediction architecture from a Neumann-series approximation under specified data models. Multiplication by missingness masks adapts computation to the observed pattern.
- **[Trees with native missing-value handling](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.HistGradientBoostingClassifier.html)** — Histogram gradient boosting learns which child receives missing values at a split. This supports prediction without a separate imputer; it does not reconstruct missing measurements.

## Evaluation and Diagnostics

- **[Imputation for prediction: beware of diminishing returns](https://proceedings.iclr.cc/paper_files/paper/2025/hash/65e837e76a5308df3d5544aab6196e21-Abstract-Conference.html)** — Le Morvan & Varoquaux (2025). Across 19 datasets, better reconstruction had limited predictive benefit with expressive predictors and missingness indicators. Results depend on the prediction setup.
- **[Missingness benchmarks](https://arxiv.org/abs/2510.02625v6)** — MissBench evaluates 42 datasets and 11 missingness patterns in the revised preprint. Report the simulated mechanism and rate; random masking alone does not establish performance under MNAR.
- **[Probabilistic evaluation](https://arxiv.org/abs/2107.03502)** — CSDI evaluates distributions with CRPS alongside point errors. For inferential multiple imputation, assess bias and interval coverage of the analysis target; low reconstruction error does not establish valid uncertainty. [Pooling assumptions](https://stefvanbuuren.github.io/fimd/sec-whyandwhen.html).
- **[Leakage control](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage)** — Fit imputers and tune their settings within training folds. Split related records or temporal windows before fitting; held-out outcomes must not become imputation predictors in deployment evaluations.
- **[Time-series masking](https://arxiv.org/abs/2107.03502)** — Evaluate isolated gaps and contiguous outages separately. Distinguish retrospective filling from online prediction: bidirectional imputers can use future observations unavailable at decision time. [BRITS](https://arxiv.org/abs/1805.10572).

## Software

- **[scikit-learn](https://scikit-learn.org/stable/modules/impute.html)** — Simple, KNN, and iterative imputers plus missingness indicators. `IterativeImputer` produces one completion per call; posterior sampling and repeated calls can generate multiple imputations.
- **[mice](https://amices.org/mice/reference/mice.html)** — Chained equations, diagnostics, and pooled inference in R. [Amelia](https://www.jstatsoft.org/article/view/v045i07) implements joint-model multiple imputation; [missForest](https://github.com/stekhoven/missForest) provides iterative forest imputation.
- **[miceforest](https://github.com/AnotherSamWilson/miceforest)** — Multiple imputation with LightGBM-based chained models and mean matching in Python. [HyperImpute](https://github.com/vanderschaarlab/hyperimpute) adds automatic column-wise model selection.
- **[MIDASpy](https://github.com/MIDASverse/MIDASpy)** — Denoising-autoencoder multiple imputation. [The MIDAS Touch](https://researchonline.lse.ac.uk/id/eprint/108170/1/Lall_Robinson_PA_Forthcoming.pdf) — Lall & Robinson (2022) — describes the method.
- **[PyPOTS](https://github.com/WenjieDu/PyPOTS)** — Implementations for learning from partially observed time series, including BRITS, SAITS, and CSDI.
- **[Impute.jl](https://github.com/invenia/Impute.jl)** — Missing-data handling for Julia vectors, matrices, and tables, including interpolation and carry-forward/backward methods.

## Related Topics

- [Bayesian Inference](https://mlpapers.org/bayesian-inference/)
- [Neural Networks](https://mlpapers.org/neural-nets/)
- [Models](https://mlpapers.org/models/)
