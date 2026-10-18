# PySpark & Pandas Lab: Breast Cancer Analysis

Course 4, Module 4 lab. It explores the Breast Cancer Wisconsin (Diagnostic) dataset with PySpark DataFrames and Spark SQL, then switches to pandas and matplotlib to plot the results.

## Contents

| File | Description |
|---|---|
| `CGLabC4M4.ipynb` | The lab notebook, Steps 0–10 |
| `breast_cancer.csv` | 569 tumor samples: an `id`, a `diagnosis` (`B` = benign, `M` = malignant) and 30 measurements such as `radius_mean`, `texture_mean` and `perimeter_mean` |

## Requirements

- Python 3.12
- Java 17 or 21, which Spark needs to run
- PySpark 3.5 or later (tested with 3.5.0 and 4.0.1)
- pandas, NumPy, matplotlib
- Jupyter, or VS Code with the Jupyter extension

## Setup

```bash
pip install pyspark pandas numpy matplotlib jupyter
```

Check that Java is available:

```bash
java -version
```

## Running the notebook

```bash
jupyter notebook CGLabC4M4.ipynb
```

Run the cells top to bottom:

- **Step 4 before Steps 5 and 7–9.** Step 4 registers the `breast_cancer` SQL view that those steps query.
- **Step 10 last.** It stops the Spark session, so later Spark cells fail until you re-run Step 0.

## What each step does

| Step | Task | Tools |
|---|---|---|
| 0 | Import libraries and start a Spark session | PySpark |
| 1 | Create the "Breast Cancer Analysis" session and confirm it is running | PySpark |
| 2 | Load the CSV, show the schema, read `perimeter_mean` from the 77th row | DataFrame API |
| 3 | Count benign and malignant cases and take the difference (B − M) | DataFrame API |
| 4 | Repeat Step 3 as a SQL query | Spark SQL |
| 5 | Build a table of cases per diagnosis and plot the class balance | Spark SQL, pandas, matplotlib |
| 6 | Summary statistics, max `compactness_mean` minus min `smoothness_mean` | `describe()`, `min`/`max` |
| 7 | Product of the rounded benign averages of radius, texture and perimeter | Spark SQL |
| 8 | Average radius-to-perimeter ratio for malignant cases | Spark SQL |
| 9 | Sum of the standard deviations of `symmetry_mean` and `fractal_dimension_mean` | Spark SQL |
| 10 | Stop the Spark session and confirm it is closed | PySpark |

## Notes

- **Extra empty column.** The CSV header ends with a trailing comma, so Spark adds an empty `_c32` column and logs a "CSV header does not conform to the schema" warning. No step uses that column. `df = df.drop("_c32")` removes it.
- **Row numbering.** Step 2 counts the 77th row from 1, which is index 76: `df.take(77)[76]`.
- **Standard deviation.** Spark SQL's `STDDEV` is the sample standard deviation (it divides by n − 1). For the population version, use `STDDEV_POP`.
