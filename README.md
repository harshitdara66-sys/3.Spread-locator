# Statistical Distribution Analysis \| Python Practical (PR-3)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)
![Status](https://img.shields.io/badge/Project-Academic%20Practical-informational)
![Domain](https://img.shields.io/badge/Domain-Statistics%20%26%20Data%20Analysis-purple)

A notebook-based statistical analysis practical exploring probability
distributions and distribution-fitting techniques using
transaction-level data. The repository contains the dataset, practical
implementation notebook, and theoretical notes.

> **Project type:** Academic / learning project\
> **Practical:** PR-3 --- Statistical Distributions\
> **Primary language:** Python

------------------------------------------------------------------------

## Table of Contents

-   [Project Overview](#project-overview)
-   [Repository Contents](#repository-contents)
-   [Dataset](#dataset)
-   [Objectives and Analysis
    Workflow](#objectives-and-analysis-workflow)
-   [Libraries and Tools](#libraries-and-tools)
-   [Environment Setup](#environment-setup)
-   [Run the Notebook](#run-the-notebook)
-   [Generated Charts](#generated-charts)
-   [Key Statistical Concepts](#key-statistical-concepts)
-   [Business Interpretation](#business-interpretation)
-   [Validation Notes](#validation-notes)
-   [Future Improvements](#future-improvements)
-   [Author](#author)

------------------------------------------------------------------------

## Project Overview

This practical studies transaction data and demonstrates how statistical
distributions can be used to describe transaction outcomes, transaction
counts, and transaction amounts.

The implementation includes:

-   Bernoulli and Binomial probability models
-   Poisson modeling of daily transaction volume
-   Log-Normal and Pareto-type Power Law distribution fitting
-   Q-Q plot for investigating normality
-   Box-Cox transformation for skewness/variance analysis
-   Z-score and probability estimation for amounts above ₹5,000
-   Probability Density Function (PDF) and Cumulative Distribution
    Function (CDF)
-   AIC comparison of fitted Log-Normal and Power Law models

The notebook is intended for educational analysis and should not be
interpreted as a production financial model.

## Repository Contents

  -----------------------------------------------------------------------
  File / Folder                       Description
  ----------------------------------- -----------------------------------
  `spread_locator_dataset.xlsx`       Transaction dataset used by the
                                      notebook

  `Practical_PR_3.ipynb`              Python practical notebook
                                      containing analysis and
                                      visualizations

  `PR_3.Theory.docx`                  Theoretical notes covering the
                                      concepts applied in the practical

  `PR_3_Charts/`                      Output directory created by the
                                      notebook for saved charts
  -----------------------------------------------------------------------

The chart directory is created automatically when the notebook runs. The
generated chart files are not necessarily included in the repository
unless committed separately.

## Dataset

The Excel workbook contains one worksheet, `spread_locator_dataset.csv`,
with **220 records and 7 fields**.

  -----------------------------------------------------------------------
  Column                              Description
  ----------------------------------- -----------------------------------
  `transaction_id`                    Unique transaction identifier

  `customer_id`                       Customer identifier

  `transaction_amount`                Transaction amount (numeric;
                                      analyzed as the main continuous
                                      variable)

  `transaction_date`                  Transaction date

  `transaction_count`                 Transaction count field used in the
                                      Binomial analysis

  `region`                            Transaction region

  `transaction_status`                Transaction outcome, such as
                                      `Success` or `Fail`
  -----------------------------------------------------------------------

The practical uses `transaction_amount`, `transaction_count`,
`transaction_status`, and `transaction_date` directly in its
calculations.

**Data note:** Confirm the date column is parsed as a datetime and that
amount values are positive before running Log-Normal fitting and Box-Cox
transformation. These methods require positive observations under the
notebook's current configuration.

## Objectives and Analysis Workflow

### 1. Bernoulli and Binomial Distributions

-   Estimates the observed success probability from
    `transaction_status`.
-   Calculates Bernoulli probabilities for the binary outcomes 0 and 1.
-   Builds a Binomial probability model using a fixed trial count of
    `n = 9` and a probability estimated from the mean of
    `transaction_count`.

### 2. Poisson Distribution

-   Groups records by transaction date.
-   Calculates the average number of records per observed day
    (`lambda`).
-   Evaluates Poisson probabilities for a range of event counts.

### 3. Log-Normal and Power Law Fitting

Fits SciPy Log-Normal and Pareto distributions to `transaction_amount`,
with the location parameter constrained to zero.

### 4. Q-Q Plot

Creates a Q-Q plot to visually compare transaction amount quantiles
against a normal reference and investigate departure from normality.

### 5. Box-Cox Transformation

Applies the Box-Cox transformation to positive transaction amounts and
compares original and transformed skewness. Histograms with KDE are
produced for visual inspection.

### 6. Z-Score and Threshold Probability

Calculates the z-score for the ₹5,000 threshold using the sample mean
and standard deviation, then estimates the upper-tail probability under
a normal model. It also calculates the empirical proportion of
observations above ₹5,000 for comparison.

### 7. PDF and CDF

Plots the fitted Log-Normal PDF against the transaction amount
distribution and produces a Log-Normal CDF curve.

### 8. Model Comparison

Computes log-likelihood and Akaike Information Criterion (AIC) for the
fitted Log-Normal and Pareto models. The lower AIC is the preferred
model among the candidates evaluated, subject to model assumptions and
fit diagnostics.

## Libraries and Tools

  -----------------------------------------------------------------------
  Tool / Library                      Usage
  ----------------------------------- -----------------------------------
  Python                              Core programming language

  Jupyter Notebook                    Interactive practical environment

  NumPy                               Numerical operations and arrays

  Pandas                              Data loading, grouping, and data
                                      manipulation

  Matplotlib                          Charting and figure export

  Seaborn                             Statistical plots and distribution
                                      visualization

  SciPy                               Probability distributions, fitting,
                                      transformations, and statistical
                                      functions

  Statsmodels                         Q-Q plot generation
  -----------------------------------------------------------------------

## Environment Setup

Recommended: Python 3.10 or later with Jupyter Notebook or JupyterLab.

Install the required packages:

``` bash
python -m pip install numpy pandas matplotlib seaborn scipy statsmodels openpyxl jupyter
```

If using a virtual environment:

``` bash
python -m venv .venv
```

Activate it:

**Windows**

``` bash
.venv\Scripts\activate
```

**macOS / Linux**

``` bash
source .venv/bin/activate
```

Then install the dependencies using the command above.

## Run the Notebook

1.  Download or clone the repository.

2.  Keep `Practical_PR_3.ipynb` and `spread_locator_dataset.xlsx` in the
    same directory.

3.  Install the dependencies.

4.  Launch Jupyter:

    ``` bash
    jupyter notebook
    ```

5.  Open `Practical_PR_3.ipynb`.

6.  Run the notebook cells from top to bottom.

The notebook creates the `PR_3_Charts` directory and saves plots there.

## Generated Charts

The notebook is configured to export visualizations including:

-   Bernoulli distribution
-   Binomial distribution
-   Poisson distribution
-   Q-Q plot for transaction amount normality
-   Original transaction amount distribution
-   Box-Cox transformed distribution
-   Log-Normal PDF
-   Log-Normal CDF

Check the output paths in the notebook for exact filenames. Some chart
filenames may need renaming for clearer documentation.

## Key Statistical Concepts

  -----------------------------------------------------------------------
  Concept                             Purpose
  ----------------------------------- -----------------------------------
  Bernoulli                           Models a single binary outcome

  Binomial                            Models successes across a fixed
                                      number of independent trials

  Poisson                             Models event counts over a defined
                                      interval

  Log-Normal                          Models positive values whose
                                      logarithms are normally distributed

  Pareto / Power Law                  Represents heavy-tailed behavior

  Q-Q Plot                            Visual diagnostic for comparing
                                      quantiles

  Box-Cox                             Transformation for positive data to
                                      reduce skewness and help stabilize
                                      variance

  Z-score                             Expresses a value in
                                      standard-deviation units from the
                                      mean

  PDF                                 Probability density of a continuous
                                      distribution

  CDF                                 Probability that a random variable
                                      is at or below a given value

  AIC                                 Model comparison criterion
                                      balancing fit and model complexity
  -----------------------------------------------------------------------

## Business Interpretation

The analysis can support exploratory questions such as:

-   What proportion of transactions succeed or fail?
-   How does daily transaction volume vary?
-   Are transaction amounts approximately normal or skewed?
-   How much probability mass lies above a selected transaction
    threshold?
-   Which of the candidate fitted distributions provides a better
    relative fit according to AIC?

Results should be interpreted alongside the dataset's size, data
quality, assumptions, and visual diagnostics. Estimated probabilities
are not guarantees about future transactions.

## Validation Notes

The README documents the files and analysis found in the supplied
notebook and supporting materials. Before using the notebook for formal
reporting, review these implementation details:

-   The Binomial section uses `n = 9` and estimates `p` as
    `transaction_count.mean() / n`; verify that the count field
    represents the intended trial process and that the resulting
    probability is between 0 and 1.
-   The Poisson section groups rows by date and counts records. This is
    a record-based daily count, not necessarily the sum of the
    `transaction_count` column.
-   The notebook saves the Poisson plot to a filename containing
    `QQ_Plot.png`; consider renaming it to `Poisson.png` to avoid
    confusion.
-   Box-Cox and the specified Log-Normal/Pareto fits require positive
    transaction amounts.
-   The Q-Q plot is a visual diagnostic; use additional statistical
    tests and domain reasoning if a formal normality conclusion is
    required.
-   AIC is meaningful for comparing models fitted to the same
    observations under compatible likelihood assumptions.

These are review recommendations, not changes automatically applied to
the submitted notebook.

## Future Improvements

-   Add a reproducible `requirements.txt` or environment file.
-   Add a data dictionary and data-quality checks.
-   Include summary statistics and missing-value checks at the start of
    the notebook.
-   Improve chart labels, units, and filenames for consistent reporting.
-   Add formal goodness-of-fit diagnostics and compare candidate models
    on a documented basis.
-   Create a concise findings section with numerical results generated
    by a fresh notebook run.

## Author

**Harshit Dara**\
Data Analytics / Python Learning Projects

------------------------------------------------------------------------

*This repository is prepared for academic learning, statistical
practice, and portfolio documentation.*
