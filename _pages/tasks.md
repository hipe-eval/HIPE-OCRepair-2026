---
title: Tasks & Data
permalink: tasks
---

## Task Overview

The ICDAR 2026 Competition on LLM-Assisted OCR Post-Correction (HIPE-OCRepair) evaluates systems that transform noisy OCR text from multilingual historical documents into clean, corrected text.

The competition provides a unified benchmark with **harmonized ground truth** and a **scoring protocol** tailored to LLM-based OCR correction. Participants are asked to build systems that, given a noisy OCR segment and its metadata, generate an improved corrected version. Both generative and hybrid approaches are supported, with a **focus on LLM-assisted methods**.

---

## Task Description

For each input text chunk (typically a paragraph-like unit), participants receive:
* The raw OCR hypothesis 
* Document-level metadata (language, publication title, type, date)
* OCR quality indicators (CER, WER, lexicon-based quality score)
* A standardized text segmentation optimized for LLMs

Systems will be evaluated on their ability to reduce character error rate (CER). More details on evaluation metrics and infrastructure can be found on the ➡️ **[Evaluation](/HIPE-OCRepair-2026/evaluation)** page.

---

## Input Format

Each item is provided as JSONL with:
* ocr: the noisy OCR text 
* metadata: language, document type, publication title, date 
* quality: CER, WER, OCR quality score 
* placeholder for corrected output

### Curation Pipeline

Because source corpora differ widely in transcription policies and quality, all development and test material undergo a rigorous harmonization workflow, including:
* Standardization of transcription rules and hyphenation conventions 
* OCR-to-GT alignment and cleanup 
* Removal of non-correctable noise (e.g., table artifacts, gibberish lines, parts of text belonging to other articles due to segmentation errors)
* Creation of semantically coherent text chunks (paragraph-like units)
* Manual verification and correction for GT consistency

---

## Datasets

We release a multilingual OCR post-correction benchmark consisting of harmonized OCR/ground truth (GT) pairs drawn from several historical collections. All datasets were processed through a unified curation pipeline that standardizes transcription conventions, segmentation, and formatting to ensure comparability across languages, periods, and document types.

The benchmark includes both:
* Training data (segmentation + formatting harmonization; original GT kept)
* Development and Test data (fully curated, standardized, manually corrected)

### 📚 Source Collections

The benchmark draws on five established datasets and two newly transcribed ones, covering newspapers, printed works, and multilingual historical materials:

| Dataset | Curation | Document Type | Languages | Period |
|--------|----------|----------------|-----------|---------|
| DTA (Deutsches Textarchiv) | medium | printed works | de | 17C–19C |
| NZZ (Neue Zürcher Zeitung) | light | newspaper | de | 19C–20C |
| ICDAR-2017 (subsets) | substantial | newspaper | fr, de | 17C–20C |
| Overproof | substantial | newspaper | en | 19C–20C |
| HIPE | newly transcribed | newspaper | en, fr, de | 19C–20C |
| Impresso | newly transcribed | newspaper | en, lu, fr, de | 19C–20C |

All data will be released under **CC-BY 4.0** and distributed via **Zenodo**, with mirrored repositories on **GitHub**.

### Realistic Example from Historical Data

Below is a simplified illustration of the four components of the HIPE-OCRepair
benchmark:  
**Original Ground Truth**, **Curated Ground Truth**, **OCR Output**, and the
**Corrected Version** a system should ideally produce.

| **Original Ground Truth**                                                        | **Curated Ground Truth** | **OCR Output** | **Corrected Version** |
|----------------------------------------------------------------------------------|---------------------------|----------------|------------------------|
| L’agence Havas nous transmet les dé pêches qui suivent…                          | L’agence Havas nous transmet les **dépêches** qui suivent… | L'agence Havas nous transmet les **dé pêches** qui suivent… | L’agence Havas nous transmet les **dépêches** qui suivent… |
| Deux bataillons d’infanterie de La Manoubaont été envoyés…                       | Deux bataillons d’infanterie de La **Manouba ont** été envoyés… | deux bataillons d'infanterie do La **Manoubaont** été envoyés… | Deux bataillons d’infanterie de La **Manouba ont** été envoyés… |
| Une vingtaine d’hommes sont descendus et se sont mis à la recherche du coupable… | Une vingtaine d’**hommes**… à la **recherche** du coupable… | une vingtaine d’**hom mes**… à la **re cherche** du coupable… | Une vingtaine d’**hommes**… à la **recherche** du coupable… |
| Après quelques instants de recherches…                                           | Après quelques instants de recherches… | Après quelques **ins-tan** de recherches… | Après quelques **instants** de recherches… |
| Les émissaires annoncent que la révolte est au camp tunisien…                    | Les émissaires annoncent que… | émissaires… **annon cent** que… | Les émissaires **annoncent** que… |
| refusent d’obéir.béir.                                                           | …refusent d’**obéir**. | …refusent d’**obéir.beir**. | …refusent d’**obéir**. |
| Le général Ben Turquia s’efforçait de calmer les mutins…                         | …s’**efforçait** de calmer les mutins… | s'**ef-.forçait** de calmer les mutins… | …s’**efforçait** de calmer les mutins… |

---

### Download Example Data

Please download the Excel file below for seven more examples and specifications on the annotation scheme.

<a href="#" class="btn btn-primary">
  Download Examples (coming soon)
</a>


---

## Baselines and Starter Code

We will provide:

- Input data in JSONL format in a repository that will be made public soon and Hugging Face dataset
- Scoring script
- A baseline system based on LLM prompting
- A Hugging Face leaderboard

Details and links will be announced soon.

---

## Questions?

Please post to [HIPE-OCRepair 2026 mailing list](https://groups.google.com/g/hipe-ocrepair-2026).
