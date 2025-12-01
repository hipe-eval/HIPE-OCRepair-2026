---
title: HIPE-OCRepair 2026
permalink: about
---

**HIPE-OCRepair** is an ICDAR 2026 competition dedicated to **OCR post-correction for multilingual historical documents**, with a particular focus on **LLM-assisted approaches**. The goal is to evaluate whether modern large language models can effectively address the **“OCR debt”** accumulated in vast digitized collections, and to provide a unified, high-quality benchmark for this long-standing challenge.

Despite major progress in OCR engines, historical documents remain difficult to digitize accurately: degraded scans, complex typography, multilingual variation, and layout noise often produce errors that propagate downstream into search, NLP, and digital humanities research. Because large-scale re-digitization is impractical for most institutions, **post-correction remains the most realistic solution**.

HIPE-OCRepair introduces a _new benchmark_, _standardized evaluation metrics_, _curated multilingual datasets_, and a _leaderboard_ to **systematically assess LLMs** and alternative approaches for OCR post-correction.

---

### Background: Why a New OCR Post-Correction Benchmark?

Previous OCR post-correction competitions ([ICDAR2017 Competition on Post-OCR Text Correction](https://l3i.univ-larochelle.fr/app/uploads/sites/12/2024/05/icdar2017-competition-post28329.pdf), [ICDAR 2019 Competition on Post-OCR Text Correction](https://hal.science/hal-02304334v1/document)) advanced the field, but limitations remain:

- inconsistent transcription policies  
- heterogeneous segmentation  
- variable annotation quality  
- lack of large-scale multilingual data  
- no unified, LLM-ready benchmark  

Meanwhile, the recent surge of LLM-based OCR post-correction studies shows both promise and **contradictory results** (please check ➡️ **[References](/HIPE-OCRepair-2026/references)**), partly because of inconsistent datasets, evaluation methods, or ground truth quality. HIPE-OCRepair addresses this gap by providing a **standardized, reproducible, community-wide benchmark**.  

---

### Benchmark

The HIPE-OCRepair benchmark provides a **unified, multilingual, and LLM-ready evaluation suite** for OCR post-correction across multiple historical collections. It is designed to capture the diversity and complexity of real-world archival material while offering consistent segmentation, metadata, and ground truth.

The benchmark includes:

- **Curated multilingual datasets** (English, French, German) covering newspapers, monographs, and other historical sources  
- **Harmonized ground truth** with consistent transcription and segmentation standards  
- **Noisy OCR inputs** aligned at the line level, the minimal and most meaningful correction unit  
- **Rich metadata** (date, collection, document type, OCR engine quality indicators) to support context-aware correction  

For details on datasets, task setup, and evaluation, see the ➡️ **[Tasks & Data](/HIPE-OCRepair-2026/tasks)** page.

---

### Evaluation Overview

More about the evaluation methodology can be found on the ➡️ **[Evaluation](/HIPE-OCRepair-2026/evaluation)** page.

---

### Registration & Participation

The full schedule, including data releases, leaderboard openings, evaluation phase, and deadlines, is available on the ➡️ **[Timeline](/HIPE-OCRepair-2026/timeline)** page.

After registration, for questions, participants may contact the organizers via the [HIPE-OCRepair 2026 mailing list](https://groups.google.com/g/hipe-ocrepair-2026).


---

### About the Organizers

**HIPE-OCRepair** is organized by members of the **[Impresso](https://impresso-project.ch/)** project (EPFL and University of Zurich), with extensive experience in historical document processing and shared tasks, including previous coordination of CLEF-HIPE 2020/2022/2026.

See the full organizer biographies on the ➡️ **[Organizers](/HIPE-OCRepair-2026/organizers)** page.

---