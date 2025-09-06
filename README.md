
## R-Project

This repository contains a single R-based analysis notebook: `data analyze and model build.ipynb`.

The README is specific to the notebook's contents (packages, dataset path, EDA results, and the modeling pipeline).

## Notebook summary

- Kernel: R
- Dataset: `GoldUP.csv` (original load path in the notebook: `/kaggle/input/r-lab3/GoldUP.csv`).
- Main steps executed in the notebook:
	- Data loading and preprocessing (Date parsing with lubridate; scaling numeric features).
	- Exploratory data analysis: summary statistics, correlation matrix and heatmap, time-series plots for numeric variables, boxplots, and Pearson correlation tests against `Gold_Price`.
	- Modeling: Random Forest regression to predict `Gold_Price` using an 80/20 train/test split.

## R packages required

Install the packages used in the notebook before running:

```r
install.packages(c(
	"readr",
	"lubridate",
	"tidyverse",
	"ggplot2",
	"reshape2",
	"dplyr",
	"randomForest",
	"caret"
))
```

## Preprocessing and modeling details

- Date parsing: `dmy(Date)` (lubridate).
- Missing values: `sum(is.na(gold_data))` returns zero in the notebook.
- Feature scaling: `mutate(across(where(is.numeric), scale))`.
- Columns removed prior to modeling: `Date`, `USD_Index`, `Interest_Rate`.
- Train/test split: 80% train, 20% test via `createDataPartition(..., p = 0.8)` with `set.seed(123)`.
- Model: `randomForest` regression with parameters from the notebook:
	- `ntree = 500`
	- `mtry = 4`
	- `importance = TRUE`
	- additional arguments: `splitrule = "variance"`, `min.node.size = 5`.

## EDA highlights (from notebook outputs)

- Strong positive correlations with `Gold_Price`: `CPI`, `Sensex`, `USD_INR`.
- Weak negative correlation with `USD_Index`.

## Run instructions (concise)

1. Install R (>= 4.0) and the R packages listed above.
2. Start Jupyter Notebook from the project folder:

```powershell
jupyter notebook
```

3. Open `data analyze and model build.ipynb` in Jupyter and select the R kernel; execute cells in order.

Alternative: open the notebook in RStudio and run cells interactively.

## Notes and actionable suggestions

- The notebook currently reads the dataset from an absolute Kaggle path (`/kaggle/input/r-lab3/GoldUP.csv`). For local execution, place `GoldUP.csv` in a `data/` folder and update the loading line to:

```r
gold_data <- read_csv("data/GoldUP.csv")
```

## License

No license file is included.
