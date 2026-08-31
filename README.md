# Misleading ChartQA

Dataset of chartQA (EMNLP 2025 Oral), designed to probe model sensitivity to common misleading visualization practices (cherry-picking, inappropriate scales, missing data, dual encoding, etc.). Each case includes a chart figure, underlying data, and multiple-choice QA with a correct option and a "misleader" option with explanation.

## Leaderboard

Results on the full public set (**n = 3,055**). All scores are accuracy percentages (higher is better), and models are ranked by Baseline accuracy.

| Rank | Model | Baseline ↑ | CoT ↑ | Pipeline ↑ |
|---:|---|---:|---:|---:|
| 1 | claude-opus-5 | **79.64** | **80.16** | **80.62** |
| 2 | gpt-5.5 | 77.51 | 77.22 | 77.09 |
| 3 | kimi-k3 | 75.22 | 74.73 | 77.91 |
| 4 | claude-opus-4-8 | 74.70 | 74.11 | 75.29 |
| 5 | gemini-2.5-pro | 73.68 | 73.91 | 74.50 |
| 6 | gemini-3-flash-preview | 73.09 | 73.75 | 73.22 |
| 7 | gemini-2.5-flash<sup>†</sup> | 72.21 | 73.09 | 70.67 |
| 8 | gpt-4.1-2025-04-14<sup>†</sup> | 72.08 | 71.00 | 73.32 |
| 9 | o4-mini-2025-04-16<sup>†</sup> | 70.02 | 70.97 | 68.38 |
| 10 | gpt-4o-2024-11-20<sup>†</sup> | 68.74 | 67.63 | 68.84 |
| 11 | claude-sonnet-4-5 | 68.61 | 69.49 | 71.91 |
| 12 | claude-haiku-4-5 | 66.35 | 65.73 | 69.82 |

<sup>†</sup> Model included in the original paper evaluation.

## Dataset (`dataset/`)

Directory layout: `code/`, `data/`, `figures/`, `qa/`. Paths follow `<misleader_type>/<plot_type>/<case_name>.<ext>`.

- **Total cases:** ~3,060  
- **Total files:** ~12,240  

### Directory structure

```
dataset/
├── code/           # HTML visualization code (one file per case)
├── data/           # CSV data files
├── figures/        # JPEG chart images
└── qa/             # JSON question-answer files (question, options, correct, wrongDueToMisleader)
```

### QA JSON schema (per case)

Each `qa/*.json` file typically contains:

- `question`: string  
- `options`: list of four option strings  
- `correct`: index of the correct answer  
- `wrongDueToMisleader`: index of the option that is tempting from the chart but wrong given the data  


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

- **Training / evaluation:** Use `dataset/figures/` as images and `dataset/qa/` as labels; align by case name (filename without extension).  
- **Reproducing charts:** Use `dataset/code/*.html` with `dataset/data/*.csv` and a local HTTP server to re-render the same charts.

## Citation & license

Please cite the original paper (https://aclanthology.org/2025.emnlp-main.695/) when using the data.
