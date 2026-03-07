# Misleading ChartQA

Dataset of chart-based QA pairs designed to probe model sensitivity to common misleading visualization practices (cherry-picking, inappropriate scales, missing data, dual encoding, etc.). Each case includes a chart figure, underlying data, and multiple-choice QA with a correct option and a "misleader" option that is plausible from the chart but wrong from the data.

## Full train set (`train/`)

The **`train/`** folder is the complete training set used for model development and evaluation.

- **Total cases:** 2,755  
- **Total files:** ~11,027 (figures, code, QA, data per case)  
- **Composition:** 393 manually-checked expansion cases + 2,362 LLM-reviewed expansion cases (same schema and quality flow).

### Directory structure

```
train/
├── code/           # HTML visualization code (one file per case)
├── data/           # CSV data files
├── figures/        # JPEG chart images
└── qa/             # JSON question-answer files (question, options, correct, wrongDueToMisleader)
```

Paths under `code/`, `data/`, `figures/`, and `qa/` follow the same hierarchy:  
`<misleader_type>/<plot_type>/<case_name>.<ext>` (e.g. `MS_inappropriate_order/bar_chart/MS_inappropriate_order_bar_chart_4.json` in `qa/`).

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

- **Training / evaluation:** Use `train/figures/` as images and `train/qa/` as labels; align by case name (filename without extension).  
- **Reproducing charts:** Use `train/code/*.html` with `train/data/*.csv` (e.g. local HTTP server) to re-render the same charts.

## Repository contents

- **`train/`** — Full train set (2,755 cases) as above.  
- **`README.md`** — This file.  
- Root-level `code/`, `data/`, `figures/`, `qa/` — Full project sources; the `train/` set is a curated subset exported for training.

## Citation & license

Please cite the dataset and follow the repository license when using the data.
