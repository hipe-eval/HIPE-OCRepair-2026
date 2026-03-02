---
title: Tasks & Data
permalink: tasks
---

## Task Description

📦 [Data repository](https://github.com/hipe-eval/HIPE-OCRepair-2026-data) (training data and documentation)    
🗒️ [Participation Guidelines](https://github.com/hipe-eval/HIPE-OCRepair-2026-data/blob/main/README-Participation-Guidelines.md)    
📈 [HIPE-OCRepair-scorer repository](https://github.com/hipe-eval/HIPE-OCRepair-scorer/)        
📊 [Evaluation repository](https://github.com/hipe-eval/HIPE-OCRepair-2026-eval) (for resuts after the competition)      
🏆 [Hugging Face Leaderboard](https://huggingface.co/spaces/hipe-ocrepair-2026-eval)  (available soon)

The ICDAR 2026 Competition on LLM-Assisted OCR Post-Correction (HIPE-OCRepair) challenges participants to correct noisy OCR transcripts from multilingual historical documents. 

Given an OCR segment and its metadata, systems must return an improved corrected version — without access to the source images.

The competition provides a **multilingual benchmark** with curated ground truth and a standardised evaluation protocol. Both generative and hybrid approaches are welcome, with a particular focus on **LLM-assisted methods**.

For each input text chunk (typically a paragraph-like unit), participants receive:
* the raw OCR hypothesis 
* document-level metadata (language, publication title, type, date)
* OCR quality indicators (CER, WER, lexicon-based quality score)

Systems are evaluated on their ability to reduce character error rate (CER). More details on metrics and evaluation infrastructure can be found on the ➡️ **[Evaluation](/HIPE-OCRepair-2026/evaluation)** page.

---


## Datasets

The benchmark comprises multilingual OCR post-correction data drawn from several historical collections, covering newspapers and printed works in English, French, and German (17th–20th century). All datasets were processed through a unified curation pipeline that standardises format, document unit segmentation and, as far as possible, transcription conventions, to ensure comparability across languages, time periods, and document types.

The benchmark includes training data (segmentation and formatting harmonisation only; original GT retained) as well as fully curated, manually corrected development and test sets.

👉 **See the [HIPE-OCRepair-2026-data repository](https://github.com/hipe-eval/HIPE-OCRepair-2026-data) to access the data and detailed documentation on the curation process.**

### 📚 Source Collections

| Dataset                             | Curation | Document Type | Languages | Period |
|-------------------------------------|----------|----------------|-----------|---------|
| DTA-19 (Deutsches Textarchiv)       | medium | printed works | de | 17C–19C |
| impresso-nzz (Neue Zürcher Zeitung) | light | newspaper | de | 19C–20C |
| ICDAR-2017 (subsets)                | substantial | newspaper | fr, de | 17C–20C |
| Overproof                           | substantial | newspaper | en | 19C–20C |
| Impresso snippets                   | newly transcribed | newspaper | en, lu, fr, de | 19C–20C |

### Input/Output Format

Each dataset is provided as a JSONL file with JSON documents following the [hipe-ocrepair.schema.json](https://github.com/hipe-eval/HIPE-OCRepair-scorer/blob/main/data/schema/hipe-ocrepair.schema.json) schema, with four top-level fields

* document_metadata: provenance and contextual information.
* ocr_hypothesis: the OCR text to be corrected
* ground_truth: the reference transcription (masked in test files).
* ocr_postcorrection_output: the field to be filled by participant systems. 

See more information on the [Participation Guidelines](https://github.com/hipe-eval/HIPE-OCRepair-2026-data/blob/main/README-Participation-Guidelines.md).

---

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

## Questions?

Please post to [HIPE-OCRepair 2026 mailing list](https://groups.google.com/g/hipe-ocrepair-2026).
