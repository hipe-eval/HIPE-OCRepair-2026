---
title: HIPE-OCRepair 2026 evaluation results
permalink: results
---

Results are in! Overall results on the test split are:

| Rank | System | Overall cMER ↓ | 95% CI | Overall Pref Macro ↑ | 95% CI | Test sets |
|------|--------|----------------|---------|----------------------|---------|----------|
| 1 | bnf-mistral_hipe-ocrepair-bench_v0.9_run1 | 0.0050 | [0.004, 0.007] | 0.9000 | [0.835, 0.952] | 8/8 |
| 2 | bnf-mistral_hipe-ocrepair-bench_v0.9_run3 | 0.0071 | [0.005, 0.009] | 0.8737 | [0.803, 0.931] | 8/8 |
| 3 | bnf-mistral_hipe-ocrepair-bench_v0.9_run2 | 0.0090 | [0.007, 0.011] | 0.8739 | [0.791, 0.942] | 8/8 |
| 4 | blocr_hipe-ocrepair-bench_v0.9_run1 | 0.0106 | [0.008, 0.013] | 0.7028 | [0.574, 0.816] | 8/8 |
| 5 | l3i_hipe-ocrepair-bench_v0.9_run1 | 0.0176 | [0.014, 0.022] | 0.3591 | [0.229, 0.486] | 8/8 |
| 8 | baseline-no-correction_hipe-ocrepair-bench_v0.9_run1 | 0.0226 | [0.019, 0.026] | 0.0000 | [0.000, 0.000] | 8/8 |

CI = Confidence Interval calculated with the bootstrap method.

Further results on individual splits and other details are in [this markdown file](https://github.com/hipe-eval/HIPE-OCRepair-2026-eval/blob/main/HIPE_OCRepair_2026_evaluation_results.md)
