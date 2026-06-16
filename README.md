# FinEOT Dataset — Sample Release

This folder contains **40 sample questions** from the **FinEOT** benchmark, a dataset for numerical question answering over financial charts using Expression-of-Thought (EoT) reasoning.

> **The full dataset will be made publicly available upon paper acceptance.**

---

## Dataset Overview

FinEOT is a financial chart question answering benchmark focused on **numerical computation** over real-world financial charts. Each question requires extracting values from a chart and applying a mathematical operation to arrive at a numeric answer.

| Property | Value |
|---|---|
| Task | Numerical QA over financial charts |
| Question type | Computation (percentage change, difference, average, sum, etc.) |
| Answer format | Numeric (integer or decimal) |
| Reasoning format | Expression-of-Thought (LaTeX mathematical expression) |
| Sources | FinChartBench, FinMME, MME-Finance |

---

## Complexity Levels

Questions are stratified into four difficulty levels based on the effort required to extract chart values and apply the correct formula:

| Level | Description |
|---|---|
| **Easy** | Values are explicitly labelled on the chart; formula is straightforward |
| **Medium** | Values require reading from axes or legends; multi-step formula |
| **Hard** | Values must be estimated from unlabelled chart elements; complex formula |
| **Hard+** | Values from dense or ambiguous chart regions; advanced multi-step reasoning |

---

## Sample Contents

This release contains **10 samples per complexity level** (40 total), stratified across source datasets.

```
appendix_samples/
├── README.md
├── fineot_samples.json       # Sample annotations
└── images/                   # Corresponding chart images (40 files)
```

### JSON Schema

Each entry in `fineot_samples.json` contains:

```json
{
  "question_id":            "unique identifier",
  "complexity":             "easy | medium | hard | hard+",
  "origin_dataset":         "FinChartBench | FinMME | MMEFinance",
  "image":                  "filename.jpg",
  "question":               "natural language question",
  "answer":                 42.5,
  "latex_expression":       "\\frac{119 - 1}{1} \\times 100",
  "placeholder_expression": "((V1 - V2) / V2) * 100",
  "values_extracted":       {"V1": 119, "V2": 1},
  "reasoning":              "ground-truth reasoning chain",
  "predictions": {
    "direct":  {"answer": 118.0,   "correct": false},
    "zs_eot":  {"answer": 11800.0, "correct": true,  "latex_expr": "..."},
    "zs_pot":  {"answer": 11800.0, "correct": true},
    "ft_eot":  {"answer": 11800.0, "correct": true,  "latex_expr": "..."}
  }
}
```

The `predictions` field includes zero-shot Direct, zero-shot EoT, zero-shot PoT, and fine-tuned EoT outputs from **Qwen3-VL-4B-Instruct**, the representative model used in the paper's error analysis.

---

## Citation

If you use these samples, please cite our paper:

```bibtex
@article{fineot2026,
  title   = {Expression-of-Thought: Numerical Reasoning over Financial Charts},
  author  = {},
  journal = {},
  year    = {2026}
}
```

> **Note:** Citation details will be updated upon publication.

---

## License

The chart images are sourced from publicly available financial chart benchmarks (FinChartBench, FinMME, MME-Finance). Annotations and reasoning chains are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Full license details will be provided with the complete dataset release.
