---
title: Tasks & Data
permalink: tasks
---

## Task Overview

HIPE-2026 is a shared task on **person–place relation extraction** from **multilingual historical texts**. The goal is to assess whether a relation holds between a person and a place mentioned in a document — and to classify that relation with respect to its **temporal scope**.

Participants are asked to build systems that, given a historical document and a set of
entities, will classify all possible `(person, place)` pairs into one of **three
evidence-based labels** for each of two relation types. The task is designed to be
tackled by generative AI systems/LLMs as well as more traditional classification approaches.

---

## Relation Types

Two relation types are to be evaluated independently:

- **`at`** – Did the person ever reside in or visit the place prior to the document's publication?
- **`isAt`** – Is the person located at the place in the **immediate temporal context** of the document?

This design supports different downstream goals — from **spatial biographies** to **historical event contextualization**.

<div style="text-align: center;">
  <img src="/HIPE-2026/assets/images/schema-temporalscope.png" alt="Motivation" style="width: 75%;"/>
</div>
---

## Input and Output Format

Each document will be provided as a JSON with:

- Full article text (OCR with possible errors)
- A list of **person entities** (de-duplicated by surface form or linked ID)
- A list of **place entities**
- Metadata (e.g., document language, publication date)

Participants must return a classification for each possible `(person, place, relation)` triple using:

- `true`: strong textual evidence supports the relation
- `probable`: plausible inference can be made from context
- `false`: no evidence or explicitly contradicted

---

### Realistic Example from Historical Data

This example illustrates a real instance of the HIPE-2026 task using an article from the _Gazette de Lausanne_ dated 1928-05-06. It involves multiple persons and places, various temporal scopes, and differing levels of textual evidence.

---

#### 📄 Article Context

<table>
  <thead>
    <tr>
      <th style="width: 50%; font-size: 0.9em;">🇫🇷 Original French OCR</th>
      <th style="width: 50%; font-size: 0.9em;">🇬🇧 Automatic English Translation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="font-size: 0.8em;">
        Pour les enfants sinistrés de Bulgarie et de Grèce, Mgr. Stéphane, archevêque de Sofia,
        vient d’adresser à l’Union internationale de secours aux enfants une dépêche, où, après avoir
        rendu hommage à cette institution, il s’exprime comme suit : La solidarité humaine se manifeste le plus
        sensiblement dans les heures critiques. Le peuple bulgare est sincèrement reconnaissant envers tous ceux
        qui, dans son épreuve actuelle, lui ont témoigné sympathie et aide. Dieu bénisse chaque effort qui
        soulagera la souffrance, surtout celle des malheureux petits.

        <br><br>

        D’autre part, l’U.I.S.E. reçoit de sa déléguée la nouvelle qu’elle a pu assurer une distribution
        quotidienne de pain à 3400 enfants dans les environs de Philippopoli et, dans la ville même,
        de pain et de thé à 2500 enfants. En outre, elle a fourni des couvertures à l’hôpital de dix baraques
        ouvert près de Philippopoli par le chef de la garnison de cette ville, le général Koutzeroff.

        <br><br>

        D’Athènes, le Dr Doxiadès, ancien ministre, président de la Ligue patriotique d’assistance aux enfants,
        télégraphie à l’U.I.S.E. : Envisageant le danger auquel sont exposés les enfants de la population de Corinthe,
        la Ligue patriotique fait appel aux généreux sentiments de l’Union pour aider et faciliter la bonne marche
        de l’œuvre de secours entreprise.
      </td>
      <td style="font-size: 0.8em;">
        For the children affected by disasters in Bulgaria and Greece, Mgr. Stéphane, Archbishop of Sofia,
        wishes to address the International Union for Child Relief with a dispatch, in which, after paying tribute
        to this institution, he expresses himself as follows: Human solidarity is most significantly manifested
        in critical hours. The Bulgarian people are sincerely grateful to all those who, in its current ordeal,
        have shown sympathy and assistance. God bless every effort that alleviates suffering, especially that
        of the unfortunate little ones.

        <br><br>

        Furthermore, the I.U.C.R. receives news from its delegate that it has been able to ensure a daily
        distribution of bread to 3,400 children in the vicinity of Philippopolis and, in the city itself,
        bread and tea to 2,500 children. In addition, it has provided blankets to the ten-barrack hospital
        opened near Philippopolis by the commander of the garrison of that city, General Koutzeroff.

        <br><br>

        From Athens, Dr. Doxiadès, former minister and president of the Patriotic League for Child Assistance,
        telegraphs to the I.U.C.R.: Considering the danger to which the children of the population of Corinth
        are exposed, the Patriotic League appeals to the generous sentiments of the Union to help and facilitate
        the smooth progress of the relief work undertaken.
      </td>
    </tr>

  </tbody>
</table>

#### 🔑 Annotated Relation Table

| Person                                                              | Place        | `at`  | `isAt` |
| ------------------------------------------------------------------- | ------------ | ----- | ------ |
| Mgr. Stéphane, archevêque de Sofia                                  | Bulgarie     | TRUE  | FALSE  |
| Mgr. Stéphane, archevêque de Sofia                                  | Grèce        | FALSE | FALSE  |
| Mgr. Stéphane, archevêque de Sofia                                  | Philippopoli | FALSE | FALSE  |
| Mgr. Stéphane, archevêque de Sofia                                  | Athènes      | FALSE | FALSE  |
| Mgr. Stéphane, archevêque de Sofia                                  | Corinthe     | FALSE | FALSE  |
| Chef de la garnison de cette ville, le général Koutzeroff           | Bulgarie     | TRUE  | TRUE   |
| Chef de la garnison de cette ville, le général Koutzeroff           | Grèce        | FALSE | FALSE  |
| Chef de la garnison de cette ville, le général Koutzeroff           | Philippopoli | TRUE  | TRUE   |
| Chef de la garnison de cette ville, le général Koutzeroff           | Athènes      | FALSE | FALSE  |
| Chef de la garnison de cette ville, le général Koutzeroff           | Corinthe     | FALSE | FALSE  |
| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Bulgarie     | FALSE | FALSE  |
| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Grèce        | TRUE  | TRUE   |
| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Philippopoli | FALSE | FALSE  |
| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Athènes      | TRUE  | TRUE   |
| Dr. Doxiadès, ancien ministre, président de la Ligue patriotique... | Corinthe     | FALSE | FALSE  |

---

### Download Example Data

Please download the Excel file below for seven more examples and specifications on the annotation scheme.

<a href="assets/example_data/annotation_examples.xlsx" download class="btn btn-primary">
  Download Examples
</a>

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

We will release two datasets for the task:

### 🧪 Development & Test Set A

- Derived mostly from the HIPE-2022 datasets
- Languages: **French, German, English, Luxembourgish**
- Contains manually validated relation labels for pre-annotated person/place entities
- Includes metadata for temporal reasoning

### 🎭 Surprise Test Set B

- Literary corpus from the **16th–18th century**
- French-language texts annotated for NER and now enriched with relation labels
  (restricted to the `at` relation type)
- Designed to evaluate **domain generalization**

All data will be released under **CC-BY 4.0** and distributed via **Zenodo**, with mirrored repositories on **GitHub**.

---

## Baselines and Starter Code

We will provide:

- Input/output templates
- Scoring script
- A baseline system based on LLM prompting
- Pre-built notebooks for data exploration

Details and links will be added here once released.

---

## Questions?

Please post to the [mailing list](https://groups.google.com/g/hipe-2026).
