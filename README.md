# README.md — *Physician Notetaker*

## Overview

This project implements an **AI-powered Physician Notetaker pipeline** that processes a physician–patient conversation and extracts structured medical information. The system performs **medical entity extraction, structured summarization, sentiment and intent analysis**, and **SOAP note generation**.

The primary objective is to demonstrate **NLP pipeline design, clinical reasoning, and explainable AI engineering practices**, rather than model accuracy alone.

---

## NLP Pipeline Architecture

```
Raw Transcript
   ↓
Speaker Segmentation (Physician / Patient)
   ↓
Medical Entity Extraction (Rule-based NER)
   ↓
Structured Medical Summary (JSON)
   ↓
Sentiment & Intent Analysis
   ↓
SOAP Note Generation (Bonus)
```

Each stage is modular and can be independently upgraded with transformer-based models in a production environment.

---

## Medical Entity Extraction

**Entities Extracted:**

* Symptoms
* Diagnosis
* Treatment
* Prognosis

**Approach:**

* Rule-based keyword matching using clinically relevant phrases
* Sentence-level extraction to avoid hallucination
* Deterministic and explainable logic

**Example:**

* “neck pain”, “back pain” → Symptoms
* “whiplash” → Diagnosis
* “physiotherapy”, “painkillers” → Treatment

This approach ensures correctness and traceability of extracted medical facts.

---

## Structured Medical Summarization

The extracted information is converted into a **structured medical report** in JSON format.

**Output Fields:**

* Patient_Name
* Symptoms
* Diagnosis
* Treatment
* Current_Status
* Prognosis

This format aligns with real-world clinical documentation and downstream healthcare workflows.

---

## Sentiment & Intent Analysis

### Sentiment Classification

Patient sentiment is classified into:

* **Anxious**
* **Neutral**
* **Reassured**

The classification is based on lexical indicators such as expressions of concern, relief, or neutrality.

### Intent Detection

Detected intents include:

* Reporting symptoms
* Seeking reassurance
* General follow-up

This helps identify patient needs and emotional state during clinical conversations.

---

## SOAP Note Generation (Bonus)

The system generates a **SOAP (Subjective, Objective, Assessment, Plan)** note directly from the transcript.

**SOAP Mapping Logic:**

* **Subjective:** Patient-reported symptoms and history
* **Objective:** Physical examination findings
* **Assessment:** Diagnosis and severity
* **Plan:** Treatment and follow-up guidance

This mirrors how clinicians document visits in real healthcare settings.

---

## Handling Ambiguous or Missing Data

* If a medical detail is **not explicitly mentioned**, it is marked as **“Not Mentioned”**
* No assumptions are made beyond the transcript
* This avoids hallucination and ensures clinical safety

---

## Environment Constraints

This project was implemented in a **restricted online Jupyter environment** where external NLP libraries (spaCy, transformers, torch) were unavailable.

To ensure:

* Reproducibility
* Safe execution
* Clear explainability

A **pure Python, rule-based NLP pipeline** was implemented.

### Production Upgrade Path

In a production environment, this pipeline can be enhanced by integrating:

* **BioBERT / ClinicalBERT** for medical NER
* **PEGASUS / BART** for medical summarization
* **Fine-tuned BERT models** for sentiment and intent detection

The current architecture is designed to support seamless model replacement.

---

## Future Improvements

* Replace rule-based NER with transformer-based medical NER
* Train sentiment models on healthcare-specific datasets (MIMIC-III, i2b2)
* Add confidence scores for extracted entities
* Support multilingual medical transcripts
* Integrate real-time audio-to-text input

---

## How to Run

1. Open `notebook/demo.ipynb`
2. Run all cells sequentially (top to bottom)
3. Generated outputs will be saved in the `output/` directory:

   * `medical_summary.json`
   * `soap_note.json`