---
title: Tasks & Data
permalink: tasks
---

## Task Overview

The ICDAR 2026 Competition on LLM-Assisted OCR Post-Correction (**HIPE-OCRepair**) focuses on improving the quality of noisy OCR text from multilingual historical documents, using approaches ranging from large language models (LLMs) to traditional sequence-to-sequence architectures.

The goal is to evaluate whether systems can transform faulty OCR outputs into clean, human-corrected text, at scale and across diverse document types, periods, and languages.
This competition introduces a unified benchmark, harmonized ground truth, and scoring protocol specifically designed for LLM-based OCR correction in historical collections.

Participants are asked to build systems that, given a noisy OCR transcript and metadata, will produce a corrected textual output for each input segment. The competition is designed to accommodate generative, discriminative, and hybrid correction approaches.

---

## Task Description

For each input text chunk (typically a paragraph-like unit), participants receive:
* The raw OCR hypothesis 
* Document-level metadata (language, publication title, type, date)
* OCR quality indicators (CER, WER, lexicon-based quality score)
* A standardized text segmentation optimized for LLMs

Systems will be evaluated on their ability to reduce character error rate (CER) and word error rate (WER) compared to human-corrected ground truth.

[//]: # (<div style="text-align: center;">)

[//]: # (  <img src="/HIPE-2026/assets/images/schema-temporalscope.png" alt="Motivation" style="width: 75%;"/>)

[//]: # (</div>)

---

## Input and Output Format

Each item is provided as JSONL with:
* ocr: the noisy OCR text 
* metadata: language, document type, publication title, date 
* quality: CER, WER, OCR quality score 
* chunk_id: identifier

Participants must return the same JSONL containing a place for the _system's post-corrected output_.

---

### Realistic Example from Historical Data

Below is a simplified illustration of the OCR post-correction task using a short excerpt from a historical newspaper. The left-hand side shows noisy OCR; the right-hand side shows the target ground truth.

(coming soon)

[//]: # (#### 📄 Article Context)

[//]: # ()
[//]: # (<table>)

[//]: # (  <thead>)

[//]: # (    <tr>)

[//]: # (      <th style="width: 50%; font-size: 0.9em;">🇫🇷 Original French OCR</th>)

[//]: # (      <th style="width: 50%; font-size: 0.9em;">🇬🇧 Automatic English Translation</th>)

[//]: # (    </tr>)

[//]: # (  </thead>)

[//]: # (  <tbody>)

[//]: # (    <tr>)

[//]: # (      <td style="font-size: 0.8em;">)

[//]: # (        Pour les enfants sinistrés de Bulgarie et de Grèce, Mgr. Stéphane, archevêque de Sofia,)

[//]: # (        vient d’adresser à l’Union internationale de secours aux enfants une dépêche, où, après avoir)

[//]: # (        rendu hommage à cette institution, il s’exprime comme suit : La solidarité humaine se manifeste le plus)

[//]: # (        sensiblement dans les heures critiques. Le peuple bulgare est sincèrement reconnaissant envers tous ceux)

[//]: # (        qui, dans son épreuve actuelle, lui ont témoigné sympathie et aide. Dieu bénisse chaque effort qui)

[//]: # (        soulagera la souffrance, surtout celle des malheureux petits.)

[//]: # ()
[//]: # (        <br><br>)

[//]: # ()
[//]: # (        D’autre part, l’U.I.S.E. reçoit de sa déléguée la nouvelle qu’elle a pu assurer une distribution)

[//]: # (        quotidienne de pain à 3400 enfants dans les environs de Philippopoli et, dans la ville même,)

[//]: # (        de pain et de thé à 2500 enfants. En outre, elle a fourni des couvertures à l’hôpital de dix baraques)

[//]: # (        ouvert près de Philippopoli par le chef de la garnison de cette ville, le général Koutzeroff.)

[//]: # ()
[//]: # (        <br><br>)

[//]: # ()
[//]: # (        D’Athènes, le Dr Doxiadès, ancien ministre, président de la Ligue patriotique d’assistance aux enfants,)

[//]: # (        télégraphie à l’U.I.S.E. : Envisageant le danger auquel sont exposés les enfants de la population de Corinthe,)

[//]: # (        la Ligue patriotique fait appel aux généreux sentiments de l’Union pour aider et faciliter la bonne marche)

[//]: # (        de l’œuvre de secours entreprise.)

[//]: # (      </td>)

[//]: # (      <td style="font-size: 0.8em;">)

[//]: # (        For the children affected by disasters in Bulgaria and Greece, Mgr. Stéphane, Archbishop of Sofia,)

[//]: # (        wishes to address the International Union for Child Relief with a dispatch, in which, after paying tribute)

[//]: # (        to this institution, he expresses himself as follows: Human solidarity is most significantly manifested)

[//]: # (        in critical hours. The Bulgarian people are sincerely grateful to all those who, in its current ordeal,)

[//]: # (        have shown sympathy and assistance. God bless every effort that alleviates suffering, especially that)

[//]: # (        of the unfortunate little ones.)

[//]: # ()
[//]: # (        <br><br>)

[//]: # ()
[//]: # (        Furthermore, the I.U.C.R. receives news from its delegate that it has been able to ensure a daily)

[//]: # (        distribution of bread to 3,400 children in the vicinity of Philippopolis and, in the city itself,)

[//]: # (        bread and tea to 2,500 children. In addition, it has provided blankets to the ten-barrack hospital)

[//]: # (        opened near Philippopolis by the commander of the garrison of that city, General Koutzeroff.)

[//]: # ()
[//]: # (        <br><br>)

[//]: # ()
[//]: # (        From Athens, Dr. Doxiadès, former minister and president of the Patriotic League for Child Assistance,)

[//]: # (        telegraphs to the I.U.C.R.: Considering the danger to which the children of the population of Corinth)

[//]: # (        are exposed, the Patriotic League appeals to the generous sentiments of the Union to help and facilitate)

[//]: # (        the smooth progress of the relief work undertaken.)

[//]: # (      </td>)

[//]: # (    </tr>)

[//]: # ()
[//]: # (  </tbody>)

[//]: # (</table>)

[//]: # ()
[//]: # (#### 🔑 Annotated Relation Table)

[//]: # ()
[//]: # (| Person                                                              | Place        | `at`  | `isAt` |)

[//]: # (| ------------------------------------------------------------------- | ------------ | ----- | ------ |)

[//]: # (| Mgr. Stéphane, archevêque de Sofia                                  | Bulgarie     | TRUE  | FALSE  |)

[//]: # (| Mgr. Stéphane, archevêque de Sofia                                  | Grèce        | FALSE | FALSE  |)

[//]: # (| Mgr. Stéphane, archevêque de Sofia                                  | Philippopoli | FALSE | FALSE  |)

[//]: # (| Mgr. Stéphane, archevêque de Sofia                                  | Athènes      | FALSE | FALSE  |)

[//]: # (| Mgr. Stéphane, archevêque de Sofia                                  | Corinthe     | FALSE | FALSE  |)

[//]: # (| Chef de la garnison de cette ville, le général Koutzeroff           | Bulgarie     | TRUE  | TRUE   |)

[//]: # (| Chef de la garnison de cette ville, le général Koutzeroff           | Grèce        | FALSE | FALSE  |)

[//]: # (| Chef de la garnison de cette ville, le général Koutzeroff           | Philippopoli | TRUE  | TRUE   |)

[//]: # (| Chef de la garnison de cette ville, le général Koutzeroff           | Athènes      | FALSE | FALSE  |)

[//]: # (| Chef de la garnison de cette ville, le général Koutzeroff           | Corinthe     | FALSE | FALSE  |)

[//]: # (| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Bulgarie     | FALSE | FALSE  |)

[//]: # (| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Grèce        | TRUE  | TRUE   |)

[//]: # (| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Philippopoli | FALSE | FALSE  |)

[//]: # (| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Athènes      | TRUE  | TRUE   |)

[//]: # (| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Corinthe     | FALSE | FALSE  |)



---

### Download Example Data

Please download the Excel file below for seven more examples and specifications on the annotation scheme.

<a href="#" class="btn btn-primary">
  Download Examples (coming soon)
</a>

[//]: # ()
[//]: # (<a href="assets/example_data/annotation_examples.xlsx" download class="btn btn-primary">)

[//]: # (  Download Examples)

[//]: # (</a>)

---

## Evaluation Profiles

To reflect different research and application priorities, HIPE-2026 will offer two profiles:

1. **Accuracy Profile**:  
   Ranking based on standard classification metrics (Precision, Recall, F1) per relation type.

2. **Efficiency Profile**:  
   Ranking based on a composite metric balancing accuracy with:
   - Model size
   - Inference time
   - Hardware usage
   - Availability as open-source or low-cost system

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

### Curation Pipeline

Because source corpora differ widely in transcription policies and quality, all development and test material undergo a rigorous harmonization workflow, including:
* Standardization of transcription rules and hyphenation conventions 
* OCR-to-GT alignment and cleanup 
* Removal of non-correctable noise (e.g., table artifacts, gibberish lines, parts of text belonging to other articles due to segmentation errors)
* Creation of semantically coherent text chunks (paragraph-like units)
* Manual verification and correction for GT consistency

---

## Baselines and Starter Code

We will provide:

- Input/output JSONL template
- Scoring script
- A baseline system based on LLM prompting

Details and links will be announced soon. Please check back or follow updates via the [mailing list](https://groups.google.com/g/hipe-ocrepair-2026).

---

## Questions?

Please post to the [mailing list](https://groups.google.com/g/hipe-2026).
