---
title: Evaluation
permalink: evaluation
---

## Evaluation Infrastructure

The HIPE-OCRepair evaluation framework is designed to ensure **fair, transparent, and reproducible assessment** of OCR post-correction systems. It supports both **LLM-based** and **traditional** approaches, and evaluates submissions along two complementary dimensions: **correction quality** and **robustness across heterogeneous historical data**.

Participants will submit system outputs for two blind test sets in a standardized JSONL format. All evaluation scripts, baseline systems, and submission templates will be released publicly to ensure reproducibility.

---

## Core Evaluation Metrics

HIPE-OCRepair uses metrics specifically suited to **historical OCR** and **multilingual text**, where spelling variation and OCR artifacts can make naïve word-based metrics misleading.

CER is the *primary evaluation measure* for HIPE-OCRepair. It is preferred over WER because historical spelling variation and segmentation differences can artificially inflate word error penalties.

We compute:
- **Corpus-level micro-averaged CER** (global performance)
- **Per-item CER** (local performance)

Both are reported with **confidence intervals** for statistical robustness.

To evaluate how consistently a system improves the noisy input, we also compute an interpretable item-level score *sᵢ*:

- **+1** if the corrected output improves CER  
- **0** if CER stays the same  
- **–1** if the system *worsens* the text

Formally:  
`sᵢ = sign(CER_inputᵢ – CER_outputᵢ)`  

This metric highlights systems that are _stable and reliable_ across diverse documents.

Additionally, we also report:
- **WER** (word error rate)
- **CER/WER per dataset**
- **Confidence intervals** for all reported scores  

---

## Submission and Scoring

### **Submission Format**
Participants submit the same provided JSONL files that have a placeholder for the system's post-corrected output.

### **Scoring**
All submissions are evaluated with:
- **official scoring scripts** (Python)
- a **public online leaderboard** (Hugging Face)

---

## Reproducibility and Resources

All datasets, scripts, and baseline systems will be released on:

- **GitHub** (evaluation scripts, scoring tools)
- **Hugging Face** (datasets + leaderboard)
- **Zenodo** (archived version for citation)  

The leaderboard will remain active after ICDAR 2026 to support long-term benchmarking and community contributions.

---

## Updates

📢 **The official GitHub repository for HIPE-OCRepair evaluation scripts and starter code will be announced soon**.  
Please check back or join our [HIPE-OCRepair 2026 mailing list](https://groups.google.com/g/hipe-ocrepair-2026) for updates.