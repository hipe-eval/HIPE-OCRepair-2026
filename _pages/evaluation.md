---
title: Evaluation
permalink: evaluation
---

## Evaluation

The HIPE-OCRepair evaluation framework is designed to ensure **fair, transparent, and reproducible assessment** of OCR post-correction systems. It supports both **LLM-based** and **traditional** approaches across multilingual historical data.

---

## Metrics

### Primary metric: cMER

All primary metrics are based on **character-level Match Error Rate (cMER)**. Unlike standard CER, cMER is bounded in \([0,1]\) because insertions are included in the denominator. 

$$\text{cMER} = \frac{S + D + I}{H + S + D + I}$$

where \(H\) = hits, \(S\) = substitutions, \(D\) = deletions, and \(I\) = insertions at the character level. A cMER of 0.05 means the hypothesis and reference differ by 5% at the character level.

### Normalization

Before scoring in the normalized setup, texts are preprocessed as follows:

- lowercased
- punctuation and other non-word characters replaced by spaces
- underscores replaced by spaces
- repeated whitespace collapsed

Evaluation is therefore **case-insensitive** and **punctuation-insensitive**, but remains sensitive to accented characters (for example, `é` and `e` are treated as different).

---

## Formal Metric Definitions

Each test dataset consists of a set of **transcription units**. All metrics are first computed at the level of individual transcription units and then aggregated across them.

### cMER and wMER

For a single transcription unit, MER is:
$$\mathrm{MER} = \frac{S + D + I}{H + S + D + I}$$

For character-level scoring this gives **cMER**; for word-level scoring (using `jiwer.process_words(...)` after normalization) this gives **wMER**.

### Micro vs. macro aggregation

For a dataset with transcription units \(i = 1, \ldots, N\):

$$\mathrm{cMER}_{\mathrm{macro}} = \frac{1}{N} \sum_{i=1}^{N} \mathrm{cMER}_{i}$$

$$\mathrm{cMER}_{\mathrm{micro}} = \frac{\sum_i S_i + \sum_i D_i + \sum_i I_i}{\sum_i H_i + \sum_i S_i + \sum_i D_i + \sum_i I_i}$$

$(\mathrm{wMER}_{\mathrm{macro}})$ and $(\mathrm{wMER}_{\mathrm{micro}})$ are defined analogously over word-level alignments.

In plain terms:

- **Micro** aggregation pools alignment counts before computing the rate, so longer transcription units contribute more weight. For example, a long newspaper article influences micro scores more than a short snippet.
- **Macro** aggregation averages transcription-unit-level scores, so every unit — long or short — contributes equally.

### Preference-based metrics

In addition to MER, the scorer reports metrics that compare each system output to the original (uncorrected) OCR. These capture whether a system *consistently* improves over the OCR baseline, rather than producing large gains on some units while degrading others.

For each transcription unit, the preference score is:

- `1` if the system is better than the raw OCR
- `0` if both are equal
- `-1` if the system is worse than the raw OCR

The reported metrics are macro averages over transcription units:

$$\mathrm{pref\_score\_cmer\_macro} = \frac{1}{N} \sum_{i=1}^{N} \mathrm{pref}_{\mathrm{cmer}}(i)$$

$$\mathrm{pref\_score\_wmer\_macro} = \frac{1}{N} \sum_{i=1}^{N} \mathrm{pref}_{\mathrm{wmer}}(i)$$

---

## Rankings

### Primary and secondary criteria

The **primary ranking metric** is **`cmer_micro`** (lower is better), computed separately for each dataset. The **secondary ranking metric** is **`pref_score_cmer_macro`** (higher is better), used as a tiebreaker: in case of identical primary scores, runs are ranked by this metric in descending order.

### Official competition ranking

The **official competition ranking** is a **weighted mean of per-test-set `cmer_micro`** across the 8 official test sets. The secondary criterion is the corresponding weighted mean of `pref_score_cmer_macro`.

The weighting scheme is chosen so that each language contributes equally regardless of how many test sets represent it:

- **English** and **French**: two test sets each, both with weight **1**
- **German**: four test sets — `impresso-snippets` with weight **1**, and `dta19-l0`, `dta19-l1`, `dta19-l2` with weight **1/3** each, so that the three DTA splits together carry the same total weight as any single other test set and German is not overrepresented in the overall ranking

Note that `impresso-nzz` and `overproof-combined` do not contribute to the official rankings because they were released publicly before the competition.

Please refer to the [Participation Guidelines](https://github.com/hipe-eval/HIPE-OCRepair-2026-data/blob/main/README-Participation-Guidelines.md) for full details.

### Per-language rankings

In addition to the overall ranking, we report **per-language rankings** computed as a weighted mean of per-test-set `cmer_micro` over the official test sets for that language:

- **English**: mean over `icdar2017` and `impresso-snippets`
- **French**: mean over `icdar2017` and `impresso-snippets`
- **German**: `impresso-snippets` with weight `1`; `dta19-l0`, `dta19-l1`, `dta19-l2` with weight `1/3` each

The secondary criterion for per-language rankings is the corresponding weighted mean of `pref_score_cmer_macro`.

### Scorer

It is possible to use the [HIPE-OCRepair-scorer](https://github.com/hipe-eval/HIPE-OCRepair-scorer) (also available as `pip install`).

## Results

Evaluation results will be available on the results page and in the HIPE-OCRepair GitHub repository (publicly released after the competition), and will be presented at ICDAR 2026.


## Submission and Scoring

Please refer to the [Participation Guidelines](https://github.com/hipe-eval/HIPE-OCRepair-2026-data/blob/main/README-Participation-Guidelines.md) for detailed instructions on formatting and submitting system outputs.


## Reproducibility and Resources

All datasets, scripts, and baseline systems will be released on:

- **GitHub** — evaluation scripts and scoring tools (primary development repository)
- **Hugging Face** — datasets and leaderboard
- **Zenodo** — versioned archival snapshot for citation (with DOI)

The leaderboard will remain active after ICDAR 2026 to support long-term benchmarking and community contributions.


## Updates

Join the [HIPE-OCRepair 2026 mailing list](https://groups.google.com/g/hipe-ocrepair-2026) for further updates.
