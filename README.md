
## R-Project

This repository contains a single R-based analysis notebook: `data analyze and model build.ipynb`.

The README below is intentionally specific to the notebook's content (packages, dataset path, EDA steps, and the modeling pipeline) rather than broad project guidance.

## Notebook summary (specific)

- Notebook kernel: R
- Dataset used: `GoldUP.csv` (loaded in the notebook from `/kaggle/input/r-lab3/GoldUP.csv`).
- Main tasks performed in the notebook:
	- Data load & preprocessing (Date parsing with lubridate, scaling numeric features).
	- Exploratory Data Analysis: summary statistics, correlation matrix and heatmap, time-series plots for each numeric variable, boxplots, and Pearson correlation tests between features and Gold_Price.
	- Modeling: Random Forest regression to predict `Gold_Price` with an 80/20 train/test split.

## R packages used (explicit)

The notebook loads the following R packages (install these before running):

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

## Key preprocessing & modeling details (exact)

- Date parsing: Date column converted with dmy(Date) (lubridate).
- Missing values: notebook checks sum(is.na(gold_data)) and reports none.
- Feature scaling: numeric features scaled using mutate(across(where(is.numeric), scale)).
- Columns removed before modeling: `Date`, `USD_Index`, and `Interest_Rate` (the notebook drops these columns prior to training).
- Train/test split: 80% train, 20% test (createDataPartition with seed 123).
- Random seed: `set.seed(123)` used for reproducibility.
- Model: randomForest regression with parameters shown in notebook:
	- ntree = 500
	- mtry = 4
	- importance = TRUE
	- splitrule = "variance", min.node.size = 5 (these are passed in the notebook's call)

## EDA findings (as recorded in the notebook)

- Strong positive correlations with Gold_Price: CPI, Sensex, USD_INR (noted in the notebook outputs).
- Weak negative correlation: USD_Index.

## How to run (concise, exact)

1. Install R >= 4.0 and the packages listed above (or use RStudio).
2. Open a terminal / PowerShell in the project folder and start Jupyter Notebook (if you prefer Jupyter):

```powershell
jupyter notebook
```

3. In the Jupyter UI, open `data analyze and model build.ipynb` and select the R kernel. Run cells top-to-bottom.

Or open the notebook in RStudio and run cells interactively.

## Notes & small suggestions

- The notebook reads the dataset from an absolute Kaggle-style path (`/kaggle/input/r-lab3/GoldUP.csv`). For local runs, place `GoldUP.csv` in a `data/` folder and update the read_csv path, for example:

```r
gold_data <- read_csv("data/GoldUP.csv")
```

- If you want, I can:
	1) Extract all library imports and create an `install_packages.R` or `requirements.txt` equivalent; or
	2) Add a short `run_instructions.md` showing how to switch the notebook to a local data path and reproduce the model results.

## License

No license file is included. Add `LICENSE` (MIT or similar) if you want to make permissions explicit.

No explicit license included. Add a `LICENSE` file (for example MIT) if you want to make licensing explicit.

### Contact / Next steps

If you want me to expand this README (for example: list exact packages used in the notebook, add environment setup, or add a `requirements.txt`/`renv` lockfile), I can read the notebook and extract imports and commands.
