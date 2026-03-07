# Misleading ChartQA

Dataset of chart-based QA pairs designed to probe model sensitivity to common misleading visualization practices (cherry-picking, inappropriate scales, missing data, dual encoding, etc.). Each case includes a chart figure, underlying data, and multiple-choice QA with a correct option and a "misleader" option that is plausible from the chart but wrong from the data.

## Train set (`train/`) and test set (`test/`)

Both **`train/`** and **`test/`** use the same directory layout: `code/`, `data/`, `figures/`, `qa/`. Paths follow `<misleader_type>/<plot_type>/<case_name>.<ext>`.

### Train set (`train/`)

Complete training set for model development and evaluation.

- **Total cases:** 2,755  
- **Total files:** ~11,027  
- **Composition:** 393 manually-checked expansion cases + 2,362 LLM-reviewed expansion cases.

### Test set (`test/`)

Test set with the same schema; originally the root-level `code/`, `data/`, `figures/`, `qa/` folders merged under `test/` for release.

- Same structure as `train/`: `code/`, `data/`, `figures/`, `qa/`.

### Directory structure (train and test)

```
train/   or   test/
├── code/           # HTML visualization code (one file per case)
├── data/           # CSV data files
├── figures/        # JPEG chart images
└── qa/             # JSON question-answer files (question, options, correct, wrongDueToMisleader)
```

### QA JSON schema (per case)

Each `qa/*.json` file typically contains:

- `question`: string  
- `options`: list of four option strings  
- `correct`: index (0–3) of the correct answer  
- `wrongDueToMisleader`: index of the option that is tempting from the chart but wrong given the data  

Other fields (e.g. task, difficulty) may be present for compatibility.

## Case categories (misleader types)

The dataset covers many misleading visualization types, including (names may use underscores, e.g. `MS_inappropriate_order`):

- Cherry Picking, Exceeding The Canvas, Small Size  
- MS Inappropriate Scale Functions / Scale Range / Inappropriate Order / Unconventional Scale Directions  
- Dual Encoding, Missing Data, Inappropriate Aggregation  
- Continuous Encoding For Categorical Data, Categorical Encoding For Continuous Data  
- Misuse Of Cumulative Relationship, Data Visual Disproportion  
- Concealed Uncertainty, Overplotting, Lack Of Legend, Lack Of Scales  
- Misleading Annotations, Missing Normalization  

Plot types include bar_chart, line_chart, area_chart, scatter_plot, pie_chart, stacked_bar_chart, choropleth_map, heatmap, etc.

## Usage

- **Training:** Use `train/figures/` as images and `train/qa/` as labels; align by case name (filename without extension).  
- **Testing:** Use `test/figures/` and `test/qa/` the same way.  
- **Reproducing charts:** Use `train/code/*.html` with `train/data/*.csv` (or `test/` equivalents) and a local HTTP server to re-render the same charts.

## Repository contents

- **`train/`** — Full train set (2,755 cases).  
- **`test/`** — Test set (same schema and layout as `train/`).  
- **`README.md`** — This file.

## Citation & license

Please cite the dataset and follow the repository license when using the data.
